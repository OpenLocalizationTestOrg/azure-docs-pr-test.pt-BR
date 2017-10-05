---
title: Gerenciar contas de armazenamento usando o Azure Explorer para Eclipse | Microsoft Docs
description: Saiba como gerenciar suas contas de armazenamento do Azure usando o Azure Explorer para Eclipse.
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
ms.openlocfilehash: 5b3014b5aca368be8ea46863c83665abde10fed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="f8027-103">Gerenciar contas de armazenamento usando o Azure Explorer para Eclipse</span><span class="sxs-lookup"><span data-stu-id="f8027-103">Manage storage accounts by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="f8027-104">O Azure Explorer, que faz parte do Kit de ferramentas do Azure para Eclipse, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar contas de armazenamento em sua conta do Azure de dentro do IDE (ambiente de desenvolvimento integrado) Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f8027-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="f8027-105">Criar uma conta de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="f8027-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="f8027-106">Para criar uma conta de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f8027-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f8027-107">Entre em sua conta do Azure usando as [Instruções de conexão para o Kit de ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="f8027-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="f8027-108">Na exibição do **Azure Explorer**, expanda o nó **Azure**, clique com o botão direito do mouse em **Contas de Armazenamento** e, em seguida, clique em **Criar Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="f8027-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Comando para Criar Conta de Armazenamento][CS01]

3. <span data-ttu-id="f8027-110">Na caixa de diálogo **Criar Conta de Armazenamento**, especifique as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8027-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Caixa de diálogo Criar Nova Conta de Armazenamento][CS02]

   * <span data-ttu-id="f8027-112">**Nome**: especifica o nome que você deseja usar para a nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8027-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="f8027-113">**Assinatura**: especifica a assinatura do Azure que deseja usar para a nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8027-113">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="f8027-114">**Grupo de Recursos**: especifica o grupo de recursos para suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="f8027-114">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="f8027-115">Selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="f8027-115">Select one of the following options:</span></span>
      * <span data-ttu-id="f8027-116">**Criar Novo**: especifica que você deseja criar um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8027-116">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="f8027-117">**Usar existente**: especifica que você selecionará em uma lista de grupos de recursos associados à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8027-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="f8027-118">**Região**: especifica a localização em que sua conta de armazenamento será criada (por exemplo, "Oeste dos EUA").</span><span class="sxs-lookup"><span data-stu-id="f8027-118">**Region**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="f8027-119">**Tipo de conta**: especifica o tipo de conta de armazenamento a criar (por exemplo, "Armazenamento de Blobs").</span><span class="sxs-lookup"><span data-stu-id="f8027-119">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="f8027-120">Para saber mais, confira [Sobre as contas de armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="f8027-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="f8027-121">**Desempenho**: especifica qual oferta de conta de armazenamento usar do editor selecionado (por exemplo "Premium").</span><span class="sxs-lookup"><span data-stu-id="f8027-121">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="f8027-122">Para saber mais, veja [Metas de desempenho e escalabilidade do Armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="f8027-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="f8027-123">**Replicação**: especifica a replicação para a conta de armazenamento (por exemplo "Zona redundante").</span><span class="sxs-lookup"><span data-stu-id="f8027-123">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="f8027-124">Para saber mais, veja [Replicação do Armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="f8027-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="f8027-125">Quando você tiver especificado todas as opções anteriores, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f8027-125">When you have specified all of the preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="f8027-126">Criar um contêiner de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="f8027-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="f8027-127">Para criar um contêiner de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f8027-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f8027-128">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na conta de armazenamento em que deseja criar um contêiner e, em seguida, clique em **Criar contêiner de blob**.</span><span class="sxs-lookup"><span data-stu-id="f8027-128">In the **Azure Explorer** view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Comando Criar contêiner de blob][CC01]

2. <span data-ttu-id="f8027-130">Na caixa de diálogo **Criar Contêiner de Blob**, especifique o nome do seu contêiner e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8027-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="f8027-131">Para saber mais sobre como nomear contêineres de armazenamento, veja [Nomenclatura e referência de contêineres, blobs e metadados].</span><span class="sxs-lookup"><span data-stu-id="f8027-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Caixa de diálogo Criar contêiner de blob][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="f8027-133">Excluir um contêiner de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="f8027-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="f8027-134">Para excluir um contêiner de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f8027-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f8027-135">Na exibição **Azure Explorer**, clique com o botão direito do mouse no contêiner de armazenamento e, em seguida, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="f8027-135">In the **Azure Explorer** view, right-click the storage container, and then click **Delete**.</span></span>

   ![Comando Excluir contêiner de armazenamento][DC01]

2. <span data-ttu-id="f8027-137">Na janela de confirmação, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8027-137">In the confirmation window, click **OK**.</span></span>

   ![Janela de confirmação de Excluir contêiner de armazenamento][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="f8027-139">Excluir uma conta de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="f8027-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="f8027-140">Para excluir uma conta de armazenamento usando o Azure Explorer, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f8027-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f8027-141">Na exibição do **Azure Explorer**, clique com o botão direito do mouse na conta de armazenamento e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="f8027-141">In the **Azure Explorer** view, right-click the storage account, and then click **Delete**.</span></span>

   ![Comando Excluir conta de armazenamento][DS01]

2. <span data-ttu-id="f8027-143">Na janela de confirmação, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8027-143">In the confirmation window, click **OK**.</span></span>

   ![Janela de confirmação de Excluir conta de armazenamento][DS02]

## <a name="next-steps"></a><span data-ttu-id="f8027-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8027-145">Next steps</span></span>
<span data-ttu-id="f8027-146">Para saber mais sobre os tamanhos, preços e contas de armazenamento do Azure, veja os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8027-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="f8027-147">[Introdução ao Armazenamento do Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="f8027-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="f8027-148">[Sobre as contas de armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="f8027-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="f8027-149">Tamanhos de conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f8027-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="f8027-150">[Tamanhos das contas de armazenamento do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="f8027-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="f8027-151">[Tamanhos das contas de armazenamento do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="f8027-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="f8027-152">Preços da conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f8027-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="f8027-153">[Preços da conta de armazenamento do Windows]</span><span class="sxs-lookup"><span data-stu-id="f8027-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="f8027-154">[Preços da conta de armazenamento do Linux]</span><span class="sxs-lookup"><span data-stu-id="f8027-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="f8027-155">Para saber mais sobre os kits de ferramentas do Azure para Java IDEs, confira os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8027-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="f8027-156">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f8027-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f8027-157">[Novidades no Kit de Ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f8027-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f8027-158">[Instalação do Kit de Ferramentas do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f8027-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f8027-159">[Instruções de conexão para o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f8027-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f8027-160">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f8027-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="f8027-161">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f8027-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f8027-162">[Novidades no Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f8027-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f8027-163">[Instalação do Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f8027-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f8027-164">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f8027-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f8027-165">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f8027-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="f8027-166">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="f8027-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="f8027-167">[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="f8027-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="f8027-168">[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="f8027-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="f8027-169">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f8027-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f8027-170">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f8027-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f8027-171">[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="f8027-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="f8027-172">[Instalação do Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="f8027-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="f8027-173">[Instruções de conexão para o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="f8027-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="f8027-174">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="f8027-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="f8027-175">[Novidades no Kit de Ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f8027-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="f8027-176">[Novidades no Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f8027-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="f8027-177">[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="f8027-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="f8027-178">[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="f8027-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="f8027-179">[Introdução ao Armazenamento do Microsoft Azure]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="f8027-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="f8027-180">[Sobre as contas de armazenamento do Azure]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="f8027-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="f8027-181">[Replicação do Armazenamento do Azure]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="f8027-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="f8027-182">[Metas de desempenho e escalabilidade do Armazenamento do Azure]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="f8027-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="f8027-183">[Nomenclatura e referência de contêineres, blobs e metadados]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="f8027-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="f8027-184">[Tamanhos das contas de armazenamento do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="f8027-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="f8027-185">[Tamanhos das contas de armazenamento do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="f8027-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="f8027-186">[Preços da conta de armazenamento do Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="f8027-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="f8027-187">[Preços da conta de armazenamento do Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="f8027-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
