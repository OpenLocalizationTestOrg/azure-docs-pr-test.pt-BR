---
title: "Instruções de entrada do Kit de ferramentas do Azure para Eclipse | Microsoft Docs"
description: Saiba como se inscrever no Microsoft Azure usando o Kit de ferramentas do Azure para Eclipse.
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
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="f0365-103">Instruções de entrada no Azure para o Kit de Ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="f0365-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="f0365-104">O Kit de ferramentas do Azure para Eclipse fornece dois métodos para entrar em sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="f0365-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="f0365-105">**Interativo** – quando você estiver usando esse método, você inserirá suas credenciais do Azure sempre que entrar na conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0365-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="f0365-106">**Automatizado** – quando você estiver usando esse método, você criará um arquivo de credenciais que conterá os dados da entidade de serviço, após o qual você poderá usar o arquivo de credenciais para entrar automaticamente em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0365-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>

<span data-ttu-id="f0365-107">As etapas nas seções a seguir descreverão como usar cada método.</span><span class="sxs-lookup"><span data-stu-id="f0365-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="f0365-108">Entrar em sua conta do Azure interativamente</span><span class="sxs-lookup"><span data-stu-id="f0365-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="f0365-109">As etapas a seguir ilustrarão como se inscrever no Azure inserindo manualmente suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0365-109">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="f0365-110">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f0365-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="f0365-111">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu do Eclipse para Entrar no Azure][I01]

1. <span data-ttu-id="f0365-113">Quando a caixa de diálogo **Entrar no Azure** for exibida, selecione **Interativo** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-113">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Caixa de diálogo Entrar][I02]

1. <span data-ttu-id="f0365-115">Quando a caixa de diálogo **Logon no Azure** for exibida, digite as credenciais do Azure e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-115">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Caixa de diálogo Logon no Azure][I03]

1. <span data-ttu-id="f0365-117">Quando a caixa de diálogo **Selecionar Assinaturas** for exibida, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0365-117">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Caixa de diálogo Selecionar Assinaturas][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="f0365-119">Sair de sua conta do Azure quando você entrou no modo interativo</span><span class="sxs-lookup"><span data-stu-id="f0365-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="f0365-120">Depois de configurar as etapas na seção anterior, você sairá automaticamente de sua conta do Azure toda vez que reiniciar o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f0365-120">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="f0365-121">No entanto, se você quiser sair de sua conta do Azure sem reiniciar o Eclipse, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f0365-121">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="f0365-122">No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.</span><span class="sxs-lookup"><span data-stu-id="f0365-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu do Eclipse para saída do Azure][L01]

1. <span data-ttu-id="f0365-124">Quando a caixa de diálogo **Saída do Azure** for exibida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="f0365-124">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Caixa de diálogo Saída do Azure][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="f0365-126">Entrar automaticamente em sua conta do Azure e criar um arquivo de credenciais para usar no futuro</span><span class="sxs-lookup"><span data-stu-id="f0365-126">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="f0365-127">As etapas a seguir lhe orientarão na criação de um arquivo de credenciais que contém os dados da entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="f0365-127">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="f0365-128">Depois de concluir essas etapas, o Eclipse usará automaticamente o arquivo de credenciais para entrar automaticamente no Azure toda vez que você abrir o projeto.</span><span class="sxs-lookup"><span data-stu-id="f0365-128">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="f0365-129">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f0365-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="f0365-130">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu do Eclipse para Entrar no Azure][A01]

1. <span data-ttu-id="f0365-132">Quando a caixa de diálogo **Entrar no Azure** for exibida, selecione **Automatizado** e, em seguida, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="f0365-132">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Caixa de diálogo Entrar][A02]

1. <span data-ttu-id="f0365-134">Quando a caixa de diálogo **Logon no Azure** for exibida, digite as credenciais do Azure e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-134">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Caixa de diálogo Logon no Azure][A03]

1. <span data-ttu-id="f0365-136">Quando a caixa de diálogo **Criar Arquivos de Autenticação** for exibida, selecione as assinaturas que deseja usar, escolha o diretório de destino e, em seguida, clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-136">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Caixa de diálogo Logon no Azure][A04]

1. <span data-ttu-id="f0365-138">A caixa de diálogo **Status de Criação da Entidade de Serviço** será exibida e, depois que os arquivos tiverem sido criados com êxito, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0365-138">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Caixa de diálogo Status de Criação da Entidade de Serviço][A05]

1. <span data-ttu-id="f0365-140">Quando a caixa de diálogo **Entrar no Azure** for exibida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-140">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Caixa de diálogo Logon no Azure][A06]

1. <span data-ttu-id="f0365-142">Quando a caixa de diálogo **Selecionar Assinaturas** for exibida, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0365-142">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="f0365-144">Sair de sua conta do Azure quando você entrou automaticamente</span><span class="sxs-lookup"><span data-stu-id="f0365-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="f0365-145">Depois de configurar as etapas na seção anterior, o Kit de ferramentas do Azure realizará sua entrada automaticamente em sua conta do Azure toda vez que você reiniciar o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f0365-145">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="f0365-146">No entanto, para sair de sua conta do Azure e impedir que o Kit de ferramentas do Azure promova sua entrada automaticamente, use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f0365-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="f0365-147">No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.</span><span class="sxs-lookup"><span data-stu-id="f0365-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu do Eclipse para saída do Azure][L01]

1. <span data-ttu-id="f0365-149">Quando a caixa de diálogo **Saída do Azure** for exibida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="f0365-149">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Caixa de diálogo Saída do Azure][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="f0365-151">Entre automaticamente em sua conta do Azure usando um arquivo de credenciais que você já criou</span><span class="sxs-lookup"><span data-stu-id="f0365-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="f0365-152">Se você sair do Azure quando você estiver usando o Eclipse, você precisará reconfigurar o Kit de ferramentas do Azure para Eclipse para usar um arquivo de credenciais criado antes que você possa entrar automaticamente em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0365-152">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="f0365-153">As etapas a seguir explicam como configurar o Kit de ferramentas do Azure para usar um arquivo de credenciais existente.</span><span class="sxs-lookup"><span data-stu-id="f0365-153">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="f0365-154">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f0365-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="f0365-155">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu do Eclipse para Entrar no Azure][A01]

1. <span data-ttu-id="f0365-157">Quando a caixa de diálogo **Entrar no Azure** for exibida, selecione **Automatizado** e, em seguida, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-157">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Caixa de diálogo Entrar][A02]

1. <span data-ttu-id="f0365-159">Quando a caixa de diálogo **Selecionar Arquivo Autenticado** for exibida, selecione um arquivo de credenciais que você criou anteriormente e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-159">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Caixa de diálogo Entrar][A08]

1. <span data-ttu-id="f0365-161">Quando a caixa de diálogo **Entrar no Azure** for exibida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="f0365-161">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Caixa de diálogo Logon no Azure][A06]

1. <span data-ttu-id="f0365-163">Quando a caixa de diálogo **Selecionar Assinaturas** for exibida, selecione as assinaturas que deseja usar e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0365-163">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="see-also"></a><span data-ttu-id="f0365-165">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f0365-165">See Also</span></span>
<span data-ttu-id="f0365-166">Para obter mais informações sobre os kits de ferramentas do Azure para Java IDEs, confira os links a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0365-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="f0365-167">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f0365-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f0365-168">[Novidades no Kit de Ferramentas do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f0365-168">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f0365-169">[Instalação do Kit de Ferramentas do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f0365-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f0365-170">*Instruções de entrada do Kit de ferramentas do Azure para Eclipse (este artigo)*</span><span class="sxs-lookup"><span data-stu-id="f0365-170">*Sign In Instructions for the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="f0365-171">[Criar um aplicativo Web Hello World para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f0365-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="f0365-172">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f0365-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f0365-173">[Novidades no Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f0365-173">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f0365-174">[Instalação do Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f0365-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f0365-175">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f0365-175">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f0365-176">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f0365-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="f0365-177">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="f0365-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="f0365-178">[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="f0365-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="f0365-179">[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="f0365-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="f0365-180">[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f0365-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f0365-181">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f0365-181">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f0365-182">[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="f0365-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="f0365-183">[Instalação do Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="f0365-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
<span data-ttu-id="f0365-184">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="f0365-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="f0365-185">[Novidades no Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f0365-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="f0365-186">[Novidades no Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f0365-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="f0365-187">[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="f0365-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="f0365-188">[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="f0365-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
