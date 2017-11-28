---
title: "contas de armazenamento aaaManage usando Olá Gerenciador do Azure para Eclipse | Microsoft Docs"
description: "Saiba como toomanage o armazenamento do Azure contas usando Olá pesquisador do Azure para Eclipse."
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
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="b7c8d-103">Gerenciar contas de armazenamento usando Olá pesquisador do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="b7c8d-103">Manage storage accounts by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="b7c8d-104">Olá Explorer do Azure, que faz parte da saudação Kit de ferramentas do Azure para Eclipse, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar contas de armazenamento em sua conta do Azure de dentro do ambiente de desenvolvimento integrado (IDE) do Olá Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="b7c8d-105">Criar uma conta de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="b7c8d-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="b7c8d-106">toocreate uma conta de armazenamento usando hello Azure Explorer Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7c8d-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="b7c8d-107">Entrar tooyour conta do Azure usando Olá [instruções entrar para Olá Kit de ferramentas do Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="b7c8d-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="b7c8d-108">Em hello **Azure Explorer** exibir, expanda Olá **Azure** nó, clique com botão direito **contas de armazenamento**e, em seguida, clique em **criar conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Comando para Criar Conta de Armazenamento][CS01]

3. <span data-ttu-id="b7c8d-110">Em Olá **criar conta de armazenamento** caixa de diálogo, especifique Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7c8d-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![Caixa de diálogo Criar Nova Conta de Armazenamento][CS02]

   * <span data-ttu-id="b7c8d-112">**Nome**: Especifica o nome Olá Olá nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="b7c8d-113">**Assinatura**: especifica Olá assinatura do Azure que você deseja toouse Olá nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-113">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="b7c8d-114">**Grupo de recursos**: Especifica o grupo de recursos de saudação para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-114">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="b7c8d-115">Selecione uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7c8d-115">Select one of hello following options:</span></span>
      * <span data-ttu-id="b7c8d-116">**Criar novo**: Especifica que você deseja toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-116">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="b7c8d-117">**Usar existente**: especifica que você selecionará em uma lista de grupos de recursos associados à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="b7c8d-118">**Região**: Especifica o local Olá onde sua conta de armazenamento será criada (por exemplo, "Oeste US").</span><span class="sxs-lookup"><span data-stu-id="b7c8d-118">**Region**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="b7c8d-119">**Tipo de conta**: Especifica o tipo de saudação do toocreate de conta de armazenamento (por exemplo, "armazenamento de Blob").</span><span class="sxs-lookup"><span data-stu-id="b7c8d-119">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="b7c8d-120">Para saber mais, confira [Sobre as contas de armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="b7c8d-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="b7c8d-121">**Desempenho**: Especifica a conta de armazenamento toouse da oferta do publicador de saudação selecionado (por exemplo, "Premium").</span><span class="sxs-lookup"><span data-stu-id="b7c8d-121">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="b7c8d-122">Para saber mais, veja [Metas de desempenho e escalabilidade do Armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="b7c8d-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="b7c8d-123">**Replicação**: Especifica a replicação Olá Olá conta de armazenamento (por exemplo, "com redundância de zona").</span><span class="sxs-lookup"><span data-stu-id="b7c8d-123">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="b7c8d-124">Para saber mais, veja [Replicação do Armazenamento do Azure].</span><span class="sxs-lookup"><span data-stu-id="b7c8d-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="b7c8d-125">Quando você tiver especificado todos Olá anterior opções, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-125">When you have specified all of hello preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="b7c8d-126">Criar um contêiner de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="b7c8d-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="b7c8d-127">toocreate um contêiner de armazenamento usando hello Azure Explorer Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7c8d-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="b7c8d-128">Em Olá **Azure Explorer** exibir, clique em conta de armazenamento Olá onde toocreate um contêiner e, em seguida, clique em **criar contêiner de blob**.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-128">In hello **Azure Explorer** view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![Comando Criar contêiner de blob][CC01]

2. <span data-ttu-id="b7c8d-130">Em Olá **criar contêiner de blob** caixa de diálogo Especificar nome de saudação para seu contêiner e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="b7c8d-131">Para saber mais sobre como nomear contêineres de armazenamento, veja [Nomenclatura e referência de contêineres, blobs e metadados].</span><span class="sxs-lookup"><span data-stu-id="b7c8d-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Caixa de diálogo Criar contêiner de blob][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="b7c8d-133">Excluir um contêiner de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="b7c8d-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="b7c8d-134">toodelete um contêiner de armazenamento usando hello Azure Explorer Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7c8d-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="b7c8d-135">Em Olá **Azure Explorer** exibir, clique o contêiner de armazenamento hello e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-135">In hello **Azure Explorer** view, right-click hello storage container, and then click **Delete**.</span></span>

   ![Comando Excluir contêiner de armazenamento][DC01]

2. <span data-ttu-id="b7c8d-137">Na janela de confirmação de saudação, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-137">In hello confirmation window, click **OK**.</span></span>

   ![Janela de confirmação de Excluir contêiner de armazenamento][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="b7c8d-139">Excluir uma conta de armazenamento no Eclipse</span><span class="sxs-lookup"><span data-stu-id="b7c8d-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="b7c8d-140">toodelete uma conta de armazenamento usando hello Azure Explorer Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7c8d-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="b7c8d-141">Em Olá **Azure Explorer** exibir, clique em conta de armazenamento hello e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-141">In hello **Azure Explorer** view, right-click hello storage account, and then click **Delete**.</span></span>

   ![Comando Excluir conta de armazenamento][DS01]

2. <span data-ttu-id="b7c8d-143">Na janela de confirmação de saudação, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b7c8d-143">In hello confirmation window, click **OK**.</span></span>

   ![Janela de confirmação de Excluir conta de armazenamento][DS02]

## <a name="next-steps"></a><span data-ttu-id="b7c8d-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7c8d-145">Next steps</span></span>
<span data-ttu-id="b7c8d-146">Para obter mais informações sobre contas de armazenamento do Azure, tamanhos e preços, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7c8d-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="b7c8d-147">[Introdução tooMicrosoft armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="b7c8d-148">[Sobre as contas de armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="b7c8d-149">Tamanhos de conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b7c8d-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="b7c8d-150">[Tamanhos das contas de armazenamento do Windows no Azure]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="b7c8d-151">[Tamanhos das contas de armazenamento do Linux no Azure]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="b7c8d-152">Preços da conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b7c8d-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="b7c8d-153">[Preços da conta de armazenamento do Windows]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="b7c8d-154">[Preços da conta de armazenamento do Linux]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="b7c8d-155">Para obter mais informações sobre kits de ferramentas do Azure para Java IDEs, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7c8d-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="b7c8d-156">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b7c8d-157">[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b7c8d-158">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b7c8d-159">[instruções entrar para Olá Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b7c8d-160">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="b7c8d-161">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b7c8d-162">[O que há de novo no hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b7c8d-163">[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b7c8d-164">[Instruções entrar para hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b7c8d-165">[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b7c8d-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="b7c8d-166">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b7c8d-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

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

[Introdução tooMicrosoft armazenamento do Azure]: /azure/storage/storage-introduction
[Sobre as contas de armazenamento do Azure]: /azure/storage/storage-create-storage-account
[Replicação do Armazenamento do Azure]: /azure/storage/storage-redundancy
[Metas de desempenho e escalabilidade do Armazenamento do Azure]: /azure/storage/storage-scalability-targets
[Nomenclatura e referência de contêineres, blobs e metadados]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tamanhos das contas de armazenamento do Windows no Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamanhos das contas de armazenamento do Linux no Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Preços da conta de armazenamento do Windows]: /pricing/details/virtual-machines/windows/
[Preços da conta de armazenamento do Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
