---
title: Gerenciar contas de armazenamento usando o Azure Explorer para IntelliJ | Microsoft Docs
description: Saiba como gerenciar suas contas de armazenamento do Azure usando o Azure Explorer para IntelliJ.
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
ms.openlocfilehash: a1b56cc2751fc43a1ad6917eca77eec460f26694
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="a61a6-103">Gerenciar contas de armazenamento usando o Azure Explorer para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a61a6-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="a61a6-104">O Azure Explorer, que faz parte do Kit de ferramentas do Azure para IntelliJ, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar contas de armazenamento em sua conta do Azure de dentro do IDE (ambiente de desenvolvimento integrado) IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="a61a6-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="a61a6-105">Criar uma conta de armazenamento no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a61a6-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="a61a6-106">Para criar uma conta de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a61a6-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="a61a6-107">Entre em sua conta do Azure usando as [Instruções de conexão para o Kit de ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="a61a6-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span> 

2. <span data-ttu-id="a61a6-108">Na exibição do **Azure Explorer**, expanda o nó **Azure**, clique com o botão direito do mouse em **Contas de Armazenamento** e, em seguida, clique em **Criar Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="a61a6-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Comando para Criar Conta de Armazenamento][CS01]

3. <span data-ttu-id="a61a6-110">Na caixa de diálogo **Criar Conta de Armazenamento**, especifique as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="a61a6-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Caixa de diálogo Criar Nova Conta de Armazenamento][CS02]

   * <span data-ttu-id="a61a6-112">**Nome**: especifica o nome que você deseja usar para a nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a61a6-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="a61a6-113">**Tipo de conta**: especifica o tipo de conta de armazenamento a criar (por exemplo, "Armazenamento de Blobs").</span><span class="sxs-lookup"><span data-stu-id="a61a6-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="a61a6-114">Para saber mais, confira [Sobre as contas de armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="a61a6-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="a61a6-115">**Desempenho**: especifica qual oferta de conta de armazenamento usar do editor selecionado (por exemplo "Premium").</span><span class="sxs-lookup"><span data-stu-id="a61a6-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="a61a6-116">Para saber mais, veja [Metas de desempenho e escalabilidade do Armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="a61a6-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="a61a6-117">**Replicação**: especifica a replicação para a conta de armazenamento (por exemplo "Zona redundante").</span><span class="sxs-lookup"><span data-stu-id="a61a6-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="a61a6-118">Para saber mais, veja [Replicação do Armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="a61a6-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="a61a6-119">**Assinatura**: especifica a assinatura do Azure que deseja usar para a nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a61a6-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="a61a6-120">**Localização**: especifica a localização em que sua conta de armazenamento será criada (por exemplo "Oeste dos EUA").</span><span class="sxs-lookup"><span data-stu-id="a61a6-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="a61a6-121">**Grupo de Recursos**: especifica o grupo de recursos para suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a61a6-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="a61a6-122">Selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="a61a6-122">Select one of the following options:</span></span>
      * <span data-ttu-id="a61a6-123">**Criar novo**: especifica que você deseja criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a61a6-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="a61a6-124">**Usar existente**: especifica que você selecionará em uma lista de grupos de recursos associados à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a61a6-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="a61a6-125">Quando você tiver especificado todas as opções anteriores, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a61a6-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="a61a6-126">Criar um contêiner de armazenamento no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a61a6-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="a61a6-127">Para criar um contêiner de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a61a6-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="a61a6-128">Na exibição do Azure Explorer, clique com o botão direito do mouse na conta de armazenamento em que deseja criar um contêiner e, em seguida, clique em **Criar contêiner de blob**.</span><span class="sxs-lookup"><span data-stu-id="a61a6-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Comando Criar contêiner de blobs][CC01]

2. <span data-ttu-id="a61a6-130">Na caixa de diálogo **Criar Contêiner de Blob**, especifique o nome do seu contêiner e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a61a6-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="a61a6-131">Para saber mais sobre como nomear contêineres de armazenamento, veja [Nomenclatura e referência de contêineres, blobs e metadados].</span><span class="sxs-lookup"><span data-stu-id="a61a6-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Caixa de Diálogo Criar Contêiner de Armazenamento][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="a61a6-133">Excluir um contêiner de armazenamento no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a61a6-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="a61a6-134">Para excluir um contêiner de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a61a6-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="a61a6-135">Na exibição Azure Explorer, clique com o botão direito do mouse no contêiner de armazenamento e, em seguida, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="a61a6-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![Comando Excluir contêiner de armazenamento][DC01]

2. <span data-ttu-id="a61a6-137">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="a61a6-137">In the confirmation window, click **Yes**.</span></span>

   ![Janela de confirmação de Excluir contêiner de armazenamento][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="a61a6-139">Excluir uma conta de armazenamento no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="a61a6-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="a61a6-140">Para excluir uma conta de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a61a6-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="a61a6-141">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na conta de armazenamento e selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="a61a6-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![Menu Excluir Conta de Armazenamento][DS01]

2. <span data-ttu-id="a61a6-143">Na janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="a61a6-143">In the confirmation window, click **Yes**.</span></span>

   ![Janela de confirmação de Excluir conta de armazenamento][DS02]

## <a name="next-steps"></a><span data-ttu-id="a61a6-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a61a6-145">Next steps</span></span>
<span data-ttu-id="a61a6-146">Para saber mais sobre os tamanhos, preços e contas de armazenamento do Azure, veja os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a61a6-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="a61a6-147">[Introdução ao Armazenamento do Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="a61a6-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="a61a6-148">[Sobre as contas de armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="a61a6-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="a61a6-149">Tamanhos de conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a61a6-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="a61a6-150">[Tamanhos das contas de armazenamento do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="a61a6-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="a61a6-151">[Tamanhos das contas de armazenamento do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="a61a6-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="a61a6-152">Preços da conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a61a6-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="a61a6-153">[Preços da conta de armazenamento do Windows]</span><span class="sxs-lookup"><span data-stu-id="a61a6-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="a61a6-154">[Preços da conta de armazenamento do Linux]</span><span class="sxs-lookup"><span data-stu-id="a61a6-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="a61a6-155">Para saber mais sobre os kits de ferramentas do Azure para Java IDEs, confira os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a61a6-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="a61a6-156">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a61a6-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a61a6-157">[Novidades no Kit de Ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a61a6-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a61a6-158">[Instalação do Kit de Ferramentas do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a61a6-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a61a6-159">[Instruções de conexão para o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a61a6-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a61a6-160">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a61a6-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="a61a6-161">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a61a6-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a61a6-162">[Novidades no Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a61a6-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a61a6-163">[Instalação do Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a61a6-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a61a6-164">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a61a6-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a61a6-165">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a61a6-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="a61a6-166">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="a61a6-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="a61a6-167">[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="a61a6-168">[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="a61a6-169">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="a61a6-170">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="a61a6-171">[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="a61a6-172">[Instalação do Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="a61a6-173">[Instruções de conexão para o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="a61a6-174">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="a61a6-175">[Novidades no Kit de Ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="a61a6-176">[Novidades no Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="a61a6-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="a61a6-177">[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="a61a6-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="a61a6-178">[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="a61a6-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="a61a6-179">[Introdução ao Armazenamento do Microsoft Azure]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="a61a6-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="a61a6-180">[Sobre as contas de armazenamento do Azure]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="a61a6-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="a61a6-181">[Replicação do Armazenamento do Azure]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="a61a6-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="a61a6-182">[Metas de desempenho e escalabilidade do Armazenamento do Azure]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="a61a6-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="a61a6-183">[Nomenclatura e referência de contêineres, blobs e metadados]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="a61a6-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="a61a6-184">[Tamanhos das contas de armazenamento do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="a61a6-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="a61a6-185">[Tamanhos das contas de armazenamento do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="a61a6-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="a61a6-186">[Preços da conta de armazenamento do Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="a61a6-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="a61a6-187">[Preços da conta de armazenamento do Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="a61a6-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
