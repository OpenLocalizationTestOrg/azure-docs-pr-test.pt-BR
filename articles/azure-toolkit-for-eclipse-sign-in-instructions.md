---
title: "aaaSign em instruções de saudação Kit de ferramentas do Azure para Eclipse | Microsoft Docs"
description: "Saiba como toosign no Microsoft Azure usando Olá Kit de ferramentas do Azure para Eclipse."
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="8e1c6-103">Entrada do Azure em instruções para Olá Kit de ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="8e1c6-103">Azure Sign In Instructions for hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="8e1c6-104">Olá Kit de ferramentas do Azure para Eclipse fornece dois métodos para entrar em sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="8e1c6-104">hello Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="8e1c6-105">**Interativo** – quando você estiver usando esse método, você inserirá suas credenciais do Azure sempre que entrar na conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="8e1c6-106">**Automatizada** - quando você estiver usando esse método, você criará um arquivo de credenciais que contém seus dados de entidade de serviço, após o qual você pode usar o hello credenciais arquivo tooautomatically logon em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use hello credentials file tooautomatically sign into your Azure account.</span></span>

<span data-ttu-id="8e1c6-107">Olá etapas Olá seções a seguir descrevem como toouse cada método.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-107">hello steps in hello following sections will describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="8e1c6-108">Entrar em sua conta do Azure interativamente</span><span class="sxs-lookup"><span data-stu-id="8e1c6-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="8e1c6-109">Olá etapas a seguir ilustrará como toosign no Azure inserindo manualmente suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-109">hello following steps will illustrate how toosign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="8e1c6-110">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="8e1c6-111">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu do Eclipse para Entrar no Azure][I01]

1. <span data-ttu-id="8e1c6-113">Olá quando **Azure entrar** caixa de diálogo é exibida, selecione **interativo**e, em seguida, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-113">When hello **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Caixa de diálogo Entrar][I02]

1. <span data-ttu-id="8e1c6-115">Olá quando **Log no Azure** caixa de diálogo for exibida, insira suas credenciais do Azure e, em seguida, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-115">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Caixa de Diálogo de Logon do Azure][I03]

1. <span data-ttu-id="8e1c6-117">Olá quando **selecione assinaturas** caixa de diálogo for exibida, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-117">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Caixa de diálogo Selecionar Assinaturas][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="8e1c6-119">Sair de sua conta do Azure quando você entrou no modo interativo</span><span class="sxs-lookup"><span data-stu-id="8e1c6-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="8e1c6-120">Depois que você configurou etapas Olá na seção anterior Olá, você será conectado automaticamente sua conta do Azure cada vez que você reinicie o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-120">After you have configured hello steps in hello previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="8e1c6-121">No entanto, se você quiser toosign fora da sua conta do Azure sem reiniciar o Eclipse, use Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-121">However, if you want toosign out of your Azure account without restarting Eclipse, use hello following steps.</span></span>

1. <span data-ttu-id="8e1c6-122">No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu do Eclipse para saída do Azure][L01]

1. <span data-ttu-id="8e1c6-124">Olá quando **Azure sair** caixa de diálogo for exibida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-124">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Caixa de diálogo Saída do Azure][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a><span data-ttu-id="8e1c6-126">Entrar em sua conta do Azure automaticamente e criar credenciais de um arquivo toouse no hello futuras</span><span class="sxs-lookup"><span data-stu-id="8e1c6-126">Signing into your Azure account automatically and creating a credentials file toouse in hello future</span></span>

<span data-ttu-id="8e1c6-127">Olá seguinte irá orientá-lo na criação de um arquivo de credenciais que contém seus dados de entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-127">hello following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="8e1c6-128">Depois de concluir essas etapas, será Eclipse automaticamente o logon use Olá credenciais arquivo tooautomatically que você no Azure cada vez que você abra seu projeto.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-128">Once you have completed these steps, Eclipse will automatically use hello credentials file tooautomatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="8e1c6-129">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="8e1c6-130">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu do Eclipse para Entrar no Azure][A01]

1. <span data-ttu-id="8e1c6-132">Olá quando **Azure entrar** caixa de diálogo é exibida, selecione **automatizada**e, em seguida, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-132">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Caixa de diálogo Entrar][A02]

1. <span data-ttu-id="8e1c6-134">Olá quando **Log no Azure** caixa de diálogo for exibida, insira suas credenciais do Azure e, em seguida, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-134">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Caixa de Diálogo de Logon do Azure][A03]

1. <span data-ttu-id="8e1c6-136">Olá quando **criar arquivos de autenticação** caixa de diálogo for exibida, assinaturas de saudação selecione deseja toouse, escolha o diretório de destino e, em seguida, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-136">When hello **Create authentication files** dialog box appears, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Caixa de Diálogo de Logon do Azure][A04]

1. <span data-ttu-id="8e1c6-138">Olá **Status de criação da entidade de serviço** caixa de diálogo será exibida e depois que os arquivos foram criados com êxito, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-138">hello **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Caixa de diálogo Status de Criação da Entidade de Serviço][A05]

1. <span data-ttu-id="8e1c6-140">Olá quando **Azure entrar** caixa de diálogo for exibida, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-140">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Caixa de Diálogo de Logon do Azure][A06]

1. <span data-ttu-id="8e1c6-142">Olá quando **selecione assinaturas** caixa de diálogo for exibida, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-142">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="8e1c6-144">Sair de sua conta do Azure quando você entrou automaticamente</span><span class="sxs-lookup"><span data-stu-id="8e1c6-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="8e1c6-145">Depois que você configurou etapas Olá na seção anterior Olá, Olá Kit de ferramentas do Azure você entrará automaticamente em sua conta do Azure cada vez que você reinicie o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-145">After you have configured hello steps in hello previous section, hello Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="8e1c6-146">No entanto, toosign fora da sua conta do Azure e impedir que o hello Kit de ferramentas do Azure você entrar automaticamente, Olá use as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, use hello following steps.</span></span>

1. <span data-ttu-id="8e1c6-147">No Eclipse, clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Sair**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu do Eclipse para saída do Azure][L01]

1. <span data-ttu-id="8e1c6-149">Olá quando **Azure sair** caixa de diálogo for exibida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-149">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Caixa de diálogo Saída do Azure][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="8e1c6-151">Entre automaticamente em sua conta do Azure usando um arquivo de credenciais que você já criou</span><span class="sxs-lookup"><span data-stu-id="8e1c6-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="8e1c6-152">Se você sair do Azure quando você estiver usando o Eclipse, você precisará Olá tooreconfigure Kit de ferramentas do Azure para Eclipse toouse um arquivo de credenciais que tiver criado antes que você pode entrar automaticamente em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-152">If you sign out of Azure when you are using Eclipse, you will need tooreconfigure hello Azure Toolkit for Eclipse toouse a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="8e1c6-153">Olá etapas a seguir orientará você pela configuração Olá Kit de ferramentas do Azure toouse um arquivo existente de credenciais.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-153">hello following steps will walk you through configuring hello Azure Toolkit toouse an existing credentials file.</span></span>

1. <span data-ttu-id="8e1c6-154">Abra seu projeto com o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="8e1c6-155">Clique em **Ferramentas**, depois clique em **Azure** e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu do Eclipse para Entrar no Azure][A01]

1. <span data-ttu-id="8e1c6-157">Olá quando **Azure entrar** caixa de diálogo é exibida, selecione **automatizada**e, em seguida, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-157">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Caixa de diálogo Entrar][A02]

1. <span data-ttu-id="8e1c6-159">Olá quando **Selecionar arquivo autenticado** caixa de diálogo for exibida, selecione um arquivo de credenciais que você criou anteriormente e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-159">When hello **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Caixa de diálogo Entrar][A08]

1. <span data-ttu-id="8e1c6-161">Olá quando **Azure entrar** caixa de diálogo for exibida, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-161">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Caixa de Diálogo de Logon do Azure][A06]

1. <span data-ttu-id="8e1c6-163">Olá quando **selecione assinaturas** caixa de diálogo for exibida, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8e1c6-163">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Caixa de diálogo Selecionar Assinaturas][A07]

## <a name="see-also"></a><span data-ttu-id="8e1c6-165">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8e1c6-165">See Also</span></span>
<span data-ttu-id="8e1c6-166">Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e1c6-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="8e1c6-167">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8e1c6-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8e1c6-168">[Novidades no Kit de ferramentas do Azure para Eclipse de saudação]</span><span class="sxs-lookup"><span data-stu-id="8e1c6-168">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8e1c6-169">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8e1c6-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8e1c6-170">*Entrada em instruções Olá Kit de ferramentas do Azure para Eclipse (Este artigo)*</span><span class="sxs-lookup"><span data-stu-id="8e1c6-170">*Sign In Instructions for hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="8e1c6-171">[Criar um aplicativo Web Hello World para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8e1c6-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="8e1c6-172">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8e1c6-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8e1c6-173">[Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]</span><span class="sxs-lookup"><span data-stu-id="8e1c6-173">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8e1c6-174">[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8e1c6-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8e1c6-175">[Entrada em instruções hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8e1c6-175">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8e1c6-176">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8e1c6-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="8e1c6-177">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="8e1c6-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Entrada em instruções hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Kit de ferramentas do Azure para Eclipse de saudação]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Kit de ferramentas do Azure para IntelliJ de saudação]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/

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
