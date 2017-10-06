---
title: "instruções aaaSign-in para hello Azure Toolkit for IntelliJ | Microsoft Docs"
description: Saiba como toosign em tooMicrosoft do Azure usando hello o Kit de ferramentas do Azure para IntelliJ.
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="e2761-103">Instruções entrar para hello Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="e2761-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="e2761-104">Olá Kit de ferramentas do Azure para IntelliJ fornece dois métodos para entrar no tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="e2761-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="e2761-105">**Interativo**: Insira suas credenciais do Azure cada vez que você entrar no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2761-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="e2761-106">**Automatizada**: criar um arquivo de credenciais que você pode usar o logon de tooautomatically em tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2761-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="e2761-107">Olá seções a seguir descrevem como toouse cada método.</span><span class="sxs-lookup"><span data-stu-id="e2761-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="e2761-108">Entrar tooyour conta do Azure de modo interativo</span><span class="sxs-lookup"><span data-stu-id="e2761-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="e2761-109">toosign em tooAzure inserindo manualmente suas credenciais do Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2761-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="e2761-110">Abra seu projeto com o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e2761-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="e2761-111">Clique em **ferramentas**, ponto muito**Azure**e, em seguida, clique em **Azure entrar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Olá IntelliJ Azure entrar no comando][I01]

3. <span data-ttu-id="e2761-113">Em Olá **Azure entrar** janela, selecione **interativo**e, em seguida, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Hello Azure entrada na janela com interativo selecionado][I02]

4. <span data-ttu-id="e2761-115">Em Olá **Log no Azure** caixa de diálogo for exibida, insira suas credenciais do Azure e, em seguida, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![janela de diálogo de logon do Azure Olá][I03]

5. <span data-ttu-id="e2761-117">Em Olá **selecione assinaturas** caixa de diálogo, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e2761-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![caixa de diálogo Selecionar assinaturas Olá][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="e2761-119">Sair de sua conta do Azure depois de entrar interativamente</span><span class="sxs-lookup"><span data-stu-id="e2761-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="e2761-120">Depois que você configurou sua conta usando Olá etapas anteriores, você será conectado automaticamente fora da sua conta do Azure cada vez que você reiniciar IntelliJ IDEIA.</span><span class="sxs-lookup"><span data-stu-id="e2761-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="e2761-121">No entanto, se você quiser toosign fora da sua conta do Azure *sem* reiniciar IntelliJ IDEIA, Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="e2761-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="e2761-122">Em IntelliJ IDEIA, em hello **ferramentas** menus, aponte muito**Azure**e, em seguida, clique em **Azure sair**.</span><span class="sxs-lookup"><span data-stu-id="e2761-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Olá comando IntelliJ Azure sair][L01]

2. <span data-ttu-id="e2761-124">Em Olá **Azure sair** janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="e2761-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![janela de Hello Azure sair confirmação][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="e2761-126">Conectar automaticamente tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="e2761-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="e2761-127">Esta seção fornece uma orientarão pela criação de um arquivo de credenciais contendo os dados de sua entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="e2761-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="e2761-128">Depois de concluir esse processo, tooautomatically Eclipse usa Olá credenciais arquivo de entrada que no tooAzure cada vez que você abra seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e2761-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="e2761-129">Abra seu projeto com o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e2761-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="e2761-130">Em Olá **ferramentas** menu ponto muito**Azure**e, em seguida, clique em **Azure entrar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Olá IntelliJ Azure entrar no comando][A01]

3. <span data-ttu-id="e2761-132">Em Olá **Azure entrar** janela, selecione **automatizada**e, em seguida, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="e2761-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Hello Azure entrada na janela com automatizado selecionada][A02]

4. <span data-ttu-id="e2761-134">Em Olá **caixa de diálogo de logon do Azure** janela, insira suas credenciais do Azure e, em seguida, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![janela de diálogo de logon do Azure Olá][A03]

5. <span data-ttu-id="e2761-136">Em Olá **criar arquivos de autenticação** janela, assinaturas de saudação selecione deseja toouse, escolha o diretório de destino e, em seguida, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![janela de criar arquivos de autenticação Olá][A04]

6. <span data-ttu-id="e2761-138">Em Olá **Status de criação da entidade de serviço** caixa de diálogo, depois que os arquivos foram criados com êxito, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e2761-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Olá caixa de diálogo Status de criação da entidade de serviço][A05]

7. <span data-ttu-id="e2761-140">Em Olá **Azure entrar** janela, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Caixa de Diálogo de Logon do Azure][A06]

8. <span data-ttu-id="e2761-142">Em Olá **selecione assinaturas** caixa de diálogo, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e2761-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![caixa de diálogo Selecionar assinaturas Olá][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="e2761-144">Sair de sua conta do Azure depois de entrar automaticamente</span><span class="sxs-lookup"><span data-stu-id="e2761-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="e2761-145">Depois que você configurou sua conta usando Olá etapas anteriores, Olá Kit de ferramentas do Azure automaticamente faz com que você no tooyour cada vez que você reiniciar IntelliJ IDEIA de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2761-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="e2761-146">No entanto, toosign fora da sua conta do Azure e evitar Olá Kit de ferramentas do Azure de conectá-lo automaticamente, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2761-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="e2761-147">Em IntelliJ IDEIA, em hello **ferramentas** menus, aponte muito**Azure**e, em seguida, clique em **Azure sair**.</span><span class="sxs-lookup"><span data-stu-id="e2761-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Olá comando IntelliJ Azure sair][L01]

2. <span data-ttu-id="e2761-149">Em Olá **Azure sair** janela de confirmação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="e2761-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![janela de Hello Azure sair confirmação][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="e2761-151">Entre no tooyour conta do Azure automaticamente usando um arquivo existente de credenciais</span><span class="sxs-lookup"><span data-stu-id="e2761-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="e2761-152">Se você assinar fora da sua conta do Azure, quando você estiver usando IntelliJ IDEIA, você deve usar um sinal de tooautomatically de arquivo de credenciais existentes em toohello conta.</span><span class="sxs-lookup"><span data-stu-id="e2761-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="e2761-153">Olá tooconfigure Kit de ferramentas do Azure para Eclipse toouse um arquivo existente de credenciais, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2761-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="e2761-154">Abra seu projeto com o IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e2761-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="e2761-155">Em Olá **ferramentas** menu ponto muito**Azure**e, em seguida, clique em **Azure entrar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Olá IntelliJ Azure entrar no comando][A01]

3. <span data-ttu-id="e2761-157">Em Olá **Azure entrar** janela, selecione **automatizada**e, em seguida, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Hello Azure entrada na janela com automatizado selecionada][A02]

4. <span data-ttu-id="e2761-159">Em Olá **Selecionar arquivo de autenticação** caixa de diálogo, selecione um arquivo de credenciais criado anteriormente e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="e2761-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![caixa de diálogo Selecionar arquivo de autenticação Olá][A08]

5. <span data-ttu-id="e2761-161">Em Olá **Azure entrar** janela, clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="e2761-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Hello Azure entrada na janela com automatizado selecionada][A06]

6. <span data-ttu-id="e2761-163">Em Olá **selecione assinaturas** caixa de diálogo, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e2761-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![caixa de diálogo Selecionar assinaturas Olá][A07]

## <a name="next-steps"></a><span data-ttu-id="e2761-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2761-165">Next steps</span></span>
<span data-ttu-id="e2761-166">Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2761-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="e2761-167">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2761-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e2761-168">[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2761-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e2761-169">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2761-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e2761-170">[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2761-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e2761-171">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e2761-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="e2761-172">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e2761-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e2761-173">[O que há de novo no hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e2761-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e2761-174">[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e2761-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e2761-175">*Instruções entrar para hello Azure Toolkit for IntelliJ* (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="e2761-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="e2761-176">[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e2761-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="e2761-177">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e2761-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[O que há de novo no hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
