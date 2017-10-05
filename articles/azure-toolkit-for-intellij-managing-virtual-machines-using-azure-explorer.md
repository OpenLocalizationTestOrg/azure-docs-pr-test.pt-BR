---
title: "Gerenciar máquinas virtuais usando o Azure Explorer para IntelliJ | Microsoft Docs"
description: "Saiba como gerenciar suas máquinas virtuais do Azure usando o Azure Explorer para IntelliJ."
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
ms.openlocfilehash: 9197580407b3509fbf9a842e1fee1e6348478c34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="c6aec-103">Gerenciar máquinas virtuais usando o Azure Explorer para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c6aec-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="c6aec-104">O Azure Explorer, que faz parte do Kit de ferramentas do Azure para IntelliJ, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar máquinas virtuais em sua conta do Azure de dentro do IDE (ambiente de desenvolvimento integrado) IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c6aec-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="c6aec-105">Criar uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c6aec-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c6aec-106">Para criar uma máquina virtual usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6aec-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="c6aec-107">Entre em sua conta do Azure usando as etapas no artigo [Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="c6aec-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="c6aec-108">Na exibição do **Azure Explorer**, expanda o nó **Azure**, clique com o botão direito do mouse em **Máquinas Virtuais** e, em seguida, clique em **Criar VM**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="c6aec-109">![O comando Criar VM][CR01]</span><span class="sxs-lookup"><span data-stu-id="c6aec-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="c6aec-110">O assistente para **Criar uma nova Máquina Virtual** é aberto.</span><span class="sxs-lookup"><span data-stu-id="c6aec-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="c6aec-111">Na caixa de diálogo **Escolha uma Assinatura**, selecione sua assinatura e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![A janela Escolha uma Assinatura][CR02]

4. <span data-ttu-id="c6aec-113">Na janela **Selecionar uma Imagem de Máquina Virtual**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c6aec-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="c6aec-114">**Localização**: especifica o local onde sua máquina virtual será criada (por exemplo, *Oeste dos EUA*).</span><span class="sxs-lookup"><span data-stu-id="c6aec-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="c6aec-115">**Imagem recomendada**: especifica que você escolherá uma imagem de uma lista abreviada de imagens usadas com frequência.</span><span class="sxs-lookup"><span data-stu-id="c6aec-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="c6aec-116">**Imagem personalizada**: especifica que você escolherá uma imagem personalizada fornecendo as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c6aec-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="c6aec-117">**Editor**: especifica o editor que criou a imagem que você usará para sua máquina virtual (por exemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="c6aec-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="c6aec-118">**Oferta**: especifica qual oferta de máquina virtual do editor selecionado será usada (por exemplo *JDK*).</span><span class="sxs-lookup"><span data-stu-id="c6aec-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="c6aec-119">**Sku**: especifica qual SKU (unidade de manutenção de estoque) da oferta selecionada será usada (por exemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="c6aec-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="c6aec-120">**No. de Versão**: especifica qual versão do SKU selecionado será usada.</span><span class="sxs-lookup"><span data-stu-id="c6aec-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![A janela Selecionar uma Imagem de Máquina Virtual][CR03]

5. <span data-ttu-id="c6aec-122">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-122">Click **Next**.</span></span> 

6. <span data-ttu-id="c6aec-123">Na janela **Configurações Básicas de Máquina Virtual**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c6aec-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="c6aec-124">**Nome da máquina virtual**: especifica o nome para sua nova máquina virtual, que deve começar com uma letra e conter somente letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="c6aec-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="c6aec-125">**Tamanho**: especifica o número de núcleos e a memória para alocar para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6aec-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="c6aec-126">**Nome de usuário**: especifica a conta de administrador a criar para gerenciar sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6aec-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="c6aec-127">**Senha** e **Confirmar**: especifica a senha para sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="c6aec-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![A janela Configurações Básicas de Máquina Virtual][CR04]

7. <span data-ttu-id="c6aec-129">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-129">Click **Next**.</span></span> 

8. <span data-ttu-id="c6aec-130">Na janela **Recursos Associados**, insira as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6aec-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="c6aec-131">**Grupo de recursos**: especifica o grupo de recursos para suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c6aec-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="c6aec-132">Selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="c6aec-132">Select one of the following options:</span></span>
      * <span data-ttu-id="c6aec-133">**Criar novo**: especifica que você deseja criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c6aec-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="c6aec-134">**Usar existente**: especifica que você quer selecionar em uma lista de grupos de recursos associados à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6aec-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![A janela Recursos Associados][CR07]

   * <span data-ttu-id="c6aec-136">**Conta de armazenamento**: especifica a conta de armazenamento que será usada para armazenar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6aec-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="c6aec-137">Escolha uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="c6aec-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="c6aec-138">Se você escolher **Criar Nova**, a caixa de diálogo a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="c6aec-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![A caixa de diálogo Criar Conta de Armazenamento][CR05]

   * <span data-ttu-id="c6aec-140">**Rede Virtual** e **Sub-rede**: especifica a rede virtual e a sub-rede as quais sua máquina virtual se conectará.</span><span class="sxs-lookup"><span data-stu-id="c6aec-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="c6aec-141">Use uma rede e sub-rede existentes, ou crie uma nova rede e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c6aec-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="c6aec-142">Se você selecionar **Criar novo**, a caixa de diálogo a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="c6aec-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![A caixa de diálogo Criar Rede Virtual][CR06]

   * <span data-ttu-id="c6aec-144">**Endereço IP público**: especifica um endereço IP externo para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6aec-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="c6aec-145">Você pode optar por criar um novo endereço IP ou, se sua máquina virtual não tiver um endereço IP público, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="c6aec-146">**Grupo de segurança de rede**: especifica um firewall de rede opcional para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c6aec-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="c6aec-147">Selecione um firewall existente ou, se sua máquina virtual não for usar um firewall de rede, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="c6aec-148">**Conjunto de disponibilidade**: especifica um conjunto de disponibilidade opcional ao qual sua máquina virtual pode pertencer.</span><span class="sxs-lookup"><span data-stu-id="c6aec-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="c6aec-149">Selecione um conjunto de disponibilidade existente, crie um novo conjunto de disponibilidade ou, se sua máquina virtual não for pertencer a um conjunto de disponibilidade, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="c6aec-150">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-150">Click **Finish**.</span></span>  
    <span data-ttu-id="c6aec-151">Sua nova máquina virtual aparece na janela de ferramentas do Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="c6aec-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Nova máquina virtual na exibição do Azure Explorer][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="c6aec-153">Reiniciar uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c6aec-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c6aec-154">Para reiniciar uma máquina virtual usando o Azure Explorer no IntelliJ, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6aec-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="c6aec-155">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![O comando Reiniciar da máquina virtual][RE01]

2. <span data-ttu-id="c6aec-157">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-157">In the confirmation window, click **Yes**.</span></span> 

   ![A janela de confirmação de reinicialização da máquina virtual][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="c6aec-159">Desligar uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c6aec-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c6aec-160">Para desligar uma máquina virtual em execução usando o Azure Explorer no IntelliJ, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6aec-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="c6aec-161">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![O comando Desligar da máquina virtual][SH01]

2. <span data-ttu-id="c6aec-163">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-163">In the confirmation window, click **Yes**.</span></span> 

   ![A janela de confirmação de desligamento da máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="c6aec-165">Excluir uma máquina virtual no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c6aec-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="c6aec-166">Para excluir uma máquina virtual usando o Azure Explorer no IntelliJ, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6aec-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="c6aec-167">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na máquina virtual e selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![O comando Excluir da máquina virtual][DE01]

2. <span data-ttu-id="c6aec-169">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c6aec-169">In the confirmation window, click **Yes**.</span></span> 

   ![A janela de confirmação de exclusão da máquina virtual][DE02]

## <a name="next-steps"></a><span data-ttu-id="c6aec-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6aec-171">Next steps</span></span>
<span data-ttu-id="c6aec-172">Para saber mais sobre os tamanhos e preços das máquinas virtuais do Azure, veja os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6aec-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="c6aec-173">Tamanhos de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="c6aec-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="c6aec-174">[Tamanhos das máquinas virtuais do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="c6aec-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="c6aec-175">[Tamanhos das máquinas virtuais do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="c6aec-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="c6aec-176">Preços de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="c6aec-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="c6aec-177">[Preços de máquinas virtuais do Windows]</span><span class="sxs-lookup"><span data-stu-id="c6aec-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="c6aec-178">[Preços de máquinas virtuais do Linux]</span><span class="sxs-lookup"><span data-stu-id="c6aec-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="c6aec-179">Para saber mais sobre os kits de ferramentas do Azure para Java IDEs, confira os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6aec-179">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="c6aec-180">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c6aec-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c6aec-181">[Novidades no Kit de Ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c6aec-181">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c6aec-182">[Instalação do Kit de Ferramentas do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c6aec-182">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c6aec-183">[Instruções de entrada para o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c6aec-183">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c6aec-184">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c6aec-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="c6aec-185">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c6aec-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c6aec-186">[Novidades no Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c6aec-186">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c6aec-187">[Instalação do Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c6aec-187">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c6aec-188">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c6aec-188">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c6aec-189">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c6aec-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="c6aec-190">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c6aec-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="c6aec-191">[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-191">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="c6aec-192">[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-192">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="c6aec-193">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-193">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="c6aec-194">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-194">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="c6aec-195">[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-195">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="c6aec-196">[Instalação do Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-196">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="c6aec-197">[Instruções de entrada para o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-197">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="c6aec-198">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-198">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="c6aec-199">[Novidades no Kit de Ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-199">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="c6aec-200">[Novidades no Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="c6aec-200">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="c6aec-201">[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="c6aec-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="c6aec-202">[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="c6aec-202">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="c6aec-203">[Tamanhos das máquinas virtuais do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="c6aec-203">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="c6aec-204">[Tamanhos das máquinas virtuais do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="c6aec-204">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="c6aec-205">[Preços de máquinas virtuais do Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="c6aec-205">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="c6aec-206">[Preços de máquinas virtuais do Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="c6aec-206">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>


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
