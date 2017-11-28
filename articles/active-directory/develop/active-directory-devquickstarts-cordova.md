---
title: "aaaAzure AD Cordova Introdução | Microsoft Docs"
description: Como toobuild um aplicativo Cordova que se integra ao AD do Azure para entrar e chama as APIs de protegidos pelo AD do Azure usando o OAuth.
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="77d89-103">Integrar o AD do Azure com um aplicativo Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="77d89-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="77d89-104">Você pode usar o Apache Cordova toodevelop HTML5/JavaScript aplicativos que podem ser executados em dispositivos móveis, como aplicativos nativos completos.</span><span class="sxs-lookup"><span data-stu-id="77d89-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="77d89-105">Com o Azure Active Directory (AD do Azure), você pode adicionar empresariais autenticação recursos tooyour Cordova de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="77d89-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="77d89-106">Um plug-in do Cordova encapsula os SDKs nativos do Azure AD em iOS, Android, Windows Store e Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="77d89-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="77d89-107">Usando o que plug-in, você pode aprimorar seu aplicativo toosupport entrar com contas do Active Directory do Windows Server de seus usuários, obter acesso tooOffice 365 e APIs do Azure e até mesmo ajudar a proteger chamadas tooyour próprio personalizado API da web.</span><span class="sxs-lookup"><span data-stu-id="77d89-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="77d89-108">Neste tutorial, usaremos Olá Apache Cordova plug-in para a biblioteca de autenticação do Active Directory (ADAL) tooimprove um aplicativo simples adicionando Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="77d89-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="77d89-109">Com apenas algumas linhas de código, autenticar um usuário e obter um token.</span><span class="sxs-lookup"><span data-stu-id="77d89-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="77d89-110">Use esse tooquery de API do Graph Olá token tooinvoke diretório e exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="77d89-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="77d89-111">Usar autenticação de toominimize do cache de token ADAL Olá solicita usuário hello.</span><span class="sxs-lookup"><span data-stu-id="77d89-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="77d89-112">toomake esses melhorias, você precisa:</span><span class="sxs-lookup"><span data-stu-id="77d89-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="77d89-113">Registrar um aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77d89-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="77d89-114">Adicione tokens do código tooyour aplicativo toorequest.</span><span class="sxs-lookup"><span data-stu-id="77d89-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="77d89-115">Adicionar código toouse Olá token para consultar Olá Graph API e exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="77d89-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="77d89-116">Criar o projeto de implantação do Cordova Olá com todas as plataformas de saudação desejado tootarget, adicionar Olá plug-in Cordova ADAL e testar a solução de saudação em emuladores.</span><span class="sxs-lookup"><span data-stu-id="77d89-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77d89-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="77d89-117">Prerequisites</span></span>
<span data-ttu-id="77d89-118">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="77d89-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="77d89-119">Um locatário do Azure AD onde você pode ter uma conta com direitos de desenvolvimento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77d89-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="77d89-120">Um ambiente de desenvolvimento que configurou toouse Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="77d89-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="77d89-121">Se você já tiver configurado, vá diretamente toostep 1.</span><span class="sxs-lookup"><span data-stu-id="77d89-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="77d89-122">Se você não tiver um locatário Azure AD, use Olá [obter instruções sobre como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="77d89-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="77d89-123">Se você não tiver o Apache Cordova configurado no seu computador, instale o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="77d89-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="77d89-124">Git</span><span class="sxs-lookup"><span data-stu-id="77d89-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="77d89-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="77d89-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="77d89-126">[Cordova CLI](https://cordova.apache.org/) (pode ser facilmente instalado por meio do gerenciador de pacotes NPM: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="77d89-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="77d89-127">Olá anterior instalações deve funcionar no hello PC e no hello Mac.</span><span class="sxs-lookup"><span data-stu-id="77d89-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="77d89-128">Cada plataforma de destino tem pré-requisitos diferentes:</span><span class="sxs-lookup"><span data-stu-id="77d89-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="77d89-129">toobuild e execute um aplicativo Tablet/PC Windows ou Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="77d89-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="77d89-130">Instale o [Visual Studio 2013 para Windows com Atualização 2 ou superior](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express ou outra versão) ou [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="77d89-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="77d89-131">toobuild e executar um aplicativo para iOS:</span><span class="sxs-lookup"><span data-stu-id="77d89-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="77d89-132">Instale o Xcode 6.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="77d89-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="77d89-133">Baixá-lo do hello [site do desenvolvedor Apple](http://developer.apple.com/downloads) ou hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="77d89-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="77d89-134">Instale o [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="77d89-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="77d89-135">Você pode usá-lo toostart iOS aplicativos no simulador de iOS da linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="77d89-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="77d89-136">(Você pode instalá-lo facilmente por meio de saudação terminal: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="77d89-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="77d89-137">toobuild e executar um aplicativo para Android:</span><span class="sxs-lookup"><span data-stu-id="77d89-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="77d89-138">Instale [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="77d89-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="77d89-139">Certifique-se de `JAVA_HOME` (variável de ambiente) está configurado corretamente de acordo com o caminho de instalação do JDK toohello (por exemplo, C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="77d89-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="77d89-140">Instalar [SDK do Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) e adicione Olá `<android-sdk-location>\tools` tooyour local (por exemplo, C:\tools\Android\android-sdk\tools) `PATH` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="77d89-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="77d89-141">Abra o Gerenciador de SDK do Android (por exemplo, via Olá terminal: `android`) e instalar:</span><span class="sxs-lookup"><span data-stu-id="77d89-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="77d89-142">*Android 5.0.1 (API 21)* SDK de plataforma</span><span class="sxs-lookup"><span data-stu-id="77d89-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="77d89-143">*Android SDK Build-tools* versão 19.1.0 ou superior</span><span class="sxs-lookup"><span data-stu-id="77d89-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="77d89-144">*Repositório de suporte do Android* (Extras)</span><span class="sxs-lookup"><span data-stu-id="77d89-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="77d89-145">Olá SDK do Android não fornece qualquer instância do emulador padrão.</span><span class="sxs-lookup"><span data-stu-id="77d89-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="77d89-146">Criar um executando `android avd` de saudação terminal e, em seguida, selecionando **criar**, se você quiser que o aplicativo do Android Olá toorun em um emulador.</span><span class="sxs-lookup"><span data-stu-id="77d89-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="77d89-147">Recomendamos um nível de API de 19 ou superior.</span><span class="sxs-lookup"><span data-stu-id="77d89-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="77d89-148">Para obter mais informações sobre opções de emulador e a criação da Android hello, consulte [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) no site de saudação Android.</span><span class="sxs-lookup"><span data-stu-id="77d89-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="77d89-149">Etapa 1: registrar um aplicativo com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="77d89-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="77d89-150">Esta etapa é opcional.</span><span class="sxs-lookup"><span data-stu-id="77d89-150">This step is optional.</span></span> <span data-ttu-id="77d89-151">Este tutorial fornece pré-provisionado valores que você pode usar toosee Olá exemplo em ação sem fazer qualquer provisionamento em seu próprio locatário.</span><span class="sxs-lookup"><span data-stu-id="77d89-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="77d89-152">No entanto, é recomendável que você execute esta etapa e se familiarizar com o processo de Olá, pois ela será necessária quando você cria seus próprios aplicativos.</span><span class="sxs-lookup"><span data-stu-id="77d89-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="77d89-153">O Azure AD emite tokens tooonly conhecido de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="77d89-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="77d89-154">Antes de usar o AD do Azure do seu aplicativo, você precisa toocreate uma entrada para ele no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="77d89-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="77d89-155">tooregister um novo aplicativo no seu locatário:</span><span class="sxs-lookup"><span data-stu-id="77d89-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="77d89-156">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77d89-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="77d89-157">Na barra superior do hello, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="77d89-157">On hello top bar, click your account.</span></span> <span data-ttu-id="77d89-158">Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77d89-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="77d89-159">Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="77d89-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="77d89-160">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="77d89-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="77d89-161">Siga os prompts de saudação e criar um **aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="77d89-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="77d89-162">(Embora os aplicativos Cordova sejam baseados em HTML, estamos criando um aplicativo cliente nativo aqui.</span><span class="sxs-lookup"><span data-stu-id="77d89-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="77d89-163">Olá **aplicativo cliente nativo** opção deve ser selecionada ou aplicativo hello não funcionará.)</span><span class="sxs-lookup"><span data-stu-id="77d89-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="77d89-164">**Nome** descreve toousers seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77d89-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="77d89-165">**URI de redirecionamento** é hello URI que usou tooreturn tokens tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77d89-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="77d89-166">Digite **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="77d89-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="77d89-167">Depois de concluir o registro, o Azure AD atribui a um aplicativo de tooyour de ID de aplicativo único.</span><span class="sxs-lookup"><span data-stu-id="77d89-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="77d89-168">Você precisará desse valor nas seções próximos hello.</span><span class="sxs-lookup"><span data-stu-id="77d89-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="77d89-169">Você pode encontrá-lo na guia do aplicativo de saudação do hello aplicativo criado recentemente.</span><span class="sxs-lookup"><span data-stu-id="77d89-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="77d89-170">toorun `DirSearchClient Sample`, conceder Olá recém-criado aplicativo permissão tooquery hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="77d89-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="77d89-171">De saudação **configurações** página, selecione **permissões necessárias**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="77d89-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="77d89-172">Olá aplicativo do Active Directory do Azure, selecione **Microsoft Graph** como Olá API e adicione Olá **acessar o diretório de hello como o usuário conectado Olá** permissão em **delegados Permissões**.</span><span class="sxs-lookup"><span data-stu-id="77d89-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="77d89-173">Isso permite que seu Olá tooquery do aplicativo Graph API para os usuários.</span><span class="sxs-lookup"><span data-stu-id="77d89-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="77d89-174">Etapa 2: Clonar o repositório de aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="77d89-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="77d89-175">O shell ou a linha de comando, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="77d89-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="77d89-176">Etapa 3: Criar um aplicativo Cordova de saudação</span><span class="sxs-lookup"><span data-stu-id="77d89-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="77d89-177">Há várias maneiras toocreate Cordova aplicativos.</span><span class="sxs-lookup"><span data-stu-id="77d89-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="77d89-178">Neste tutorial, vamos usar interface de linha de comando Cordova hello (CLI).</span><span class="sxs-lookup"><span data-stu-id="77d89-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="77d89-179">O shell ou a linha de comando, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="77d89-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="77d89-180">Esse comando cria a estrutura de pasta de saudação e scaffolding de projeto do Cordova hello.</span><span class="sxs-lookup"><span data-stu-id="77d89-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="77d89-181">Mova a nova pasta de DirSearchClient toohello:</span><span class="sxs-lookup"><span data-stu-id="77d89-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="77d89-182">Copie o conteúdo de saudação do projeto de starter Olá na subpasta de www hello usando um Gerenciador de arquivos ou Olá seguinte comando no shell:</span><span class="sxs-lookup"><span data-stu-id="77d89-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="77d89-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="77d89-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="77d89-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="77d89-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="77d89-185">Adicione lista branca de saudação plug-in.</span><span class="sxs-lookup"><span data-stu-id="77d89-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="77d89-186">Isso é necessário para chamar hello API do Graph.</span><span class="sxs-lookup"><span data-stu-id="77d89-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="77d89-187">Adicione todas as plataformas de saudação que você deseja toosupport.</span><span class="sxs-lookup"><span data-stu-id="77d89-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="77d89-188">toohave um exemplo de funcionamento, você precisa tooexecute pelo menos um dos comandos a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="77d89-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="77d89-189">Observe que você não ser capaz de tooemulate iOS no Windows ou emular Windows em um Mac.</span><span class="sxs-lookup"><span data-stu-id="77d89-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="77d89-190">Adicione hello ADAL para o projeto do Cordova tooyour plug-in:</span><span class="sxs-lookup"><span data-stu-id="77d89-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="77d89-191">Etapa 4: Adicionar código tooauthenticate usuários e obter tokens do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="77d89-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="77d89-192">aplicativo Hello que você está desenvolvendo neste tutorial fornecerá um recurso de pesquisa de diretório simples.</span><span class="sxs-lookup"><span data-stu-id="77d89-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="77d89-193">usuário Olá pode, em seguida, digite o alias de saudação de qualquer usuário no diretório hello e visualizar alguns atributos básicos.</span><span class="sxs-lookup"><span data-stu-id="77d89-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="77d89-194">projeto de starter Olá contém a definição de saudação da interface de usuário básica de saudação do aplicativo hello (em www/index.html) e scaffolding Olá que conecta os eventos de aplicativo básico ciclos, associações de interface do usuário e resultados de lógica de exibição (em www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="77d89-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="77d89-195">Olá única tarefa para você é tooadd lógica de saudação que implementa as tarefas de identidade.</span><span class="sxs-lookup"><span data-stu-id="77d89-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="77d89-196">Olá primeira coisa toodo em seu código é apresentar valores de protocolo de saudação do AD do Azure usa para identificar seu aplicativo e Olá recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="77d89-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="77d89-197">Esses valores serão usados tooconstruct Olá solicitações de token posteriormente.</span><span class="sxs-lookup"><span data-stu-id="77d89-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="77d89-198">Inserir saudação seguindo o trecho de código na parte superior de saudação do arquivo de js hello:</span><span class="sxs-lookup"><span data-stu-id="77d89-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="77d89-199">Olá `redirectUri` e `clientId` valores devem corresponder a valores de saudação que descrevem seu aplicativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="77d89-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="77d89-200">Você pode encontrar os da saudação **configurar** guia Olá portal do Azure, conforme descrito na etapa 1, anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="77d89-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="77d89-201">Se você tiver optado por não registrar um novo aplicativo no seu próprio locatário, você pode colar apenas valores hello pré-configurado como está.</span><span class="sxs-lookup"><span data-stu-id="77d89-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="77d89-202">Você pode ver executando o exemplo hello, embora você sempre deve criar sua própria entrada para os aplicativos que são destinados a produção.</span><span class="sxs-lookup"><span data-stu-id="77d89-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="77d89-203">Em seguida, adicione o código de solicitação de token hello.</span><span class="sxs-lookup"><span data-stu-id="77d89-203">Next, add hello token request code.</span></span> <span data-ttu-id="77d89-204">Inserir saudação trecho de código a seguir entre hello `search` e `renderData` definições:</span><span class="sxs-lookup"><span data-stu-id="77d89-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="77d89-205">Vamos examinar essa função, separando-a em suas duas partes principais.</span><span class="sxs-lookup"><span data-stu-id="77d89-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="77d89-206">Este exemplo é projetado toowork com qualquer locatário, conforme toobeing contrário vinculado tooa um determinado.</span><span class="sxs-lookup"><span data-stu-id="77d89-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="77d89-207">Ele usa hello "/ comum" ponto de extremidade, que permite que Olá usuário tooenter qualquer conta no momento da autenticação e direciona o locatário do hello solicitação toohello qual ele pertence.</span><span class="sxs-lookup"><span data-stu-id="77d89-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="77d89-208">Esta primeira parte do método hello inspeciona Olá cache ADAL toosee se um token já está armazenado.</span><span class="sxs-lookup"><span data-stu-id="77d89-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="77d89-209">Nesse caso, o método hello usa locatários Olá onde token Olá veio para reinicializar ADAL.</span><span class="sxs-lookup"><span data-stu-id="77d89-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="77d89-210">Isso é necessário tooavoid prompts extras, porque Olá uso de "/ comum" sempre resulta em perguntando Olá usuário tooenter uma nova conta.</span><span class="sxs-lookup"><span data-stu-id="77d89-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="77d89-211">a segunda parte saudação do método hello executa Olá solicitação de token adequado.</span><span class="sxs-lookup"><span data-stu-id="77d89-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="77d89-212">Olá `acquireTokenSilentAsync` método solicita tooreturn ADAL um token Olá especificado recursos sem mostrar qualquer UX.</span><span class="sxs-lookup"><span data-stu-id="77d89-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="77d89-213">Que pode acontecer se o cache Olá já tem um token de acesso adequado armazenado, ou se um token de atualização pode ser usado tooget um novo token de acesso sem mostrar qualquer prompt.</span><span class="sxs-lookup"><span data-stu-id="77d89-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="77d89-214">Se essa tentativa falhar, podemos voltar aos `acquireTokenAsync`– que solicitará visivelmente Olá tooauthenticate de usuário.</span><span class="sxs-lookup"><span data-stu-id="77d89-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="77d89-215">Agora que temos token hello, podemos finalmente invocar Olá API do Graph e executar a consulta de pesquisa de saudação que queremos.</span><span class="sxs-lookup"><span data-stu-id="77d89-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="77d89-216">Inserir saudação seguindo o trecho abaixo Olá `authenticate` definição:</span><span class="sxs-lookup"><span data-stu-id="77d89-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="77d89-217">arquivos de ponto inicial de saudação fornecido um simple UX para inserir o alias do usuário na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="77d89-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="77d89-218">Esse método usará esse valor tooconstruct uma consulta, combiná-lo com o token de acesso do hello, enviá-lo tooMicrosoft gráfico e analisar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="77d89-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="77d89-219">Olá `renderData` método, já está presente no arquivo de ponto inicial de hello, cuida de visualizar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="77d89-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="77d89-220">Etapa 5: Executar aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="77d89-220">Step 5: Run hello app</span></span>
<span data-ttu-id="77d89-221">Seu aplicativo é toorun finalmente pronto.</span><span class="sxs-lookup"><span data-stu-id="77d89-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="77d89-222">Operacional ele é simple: quando o aplicativo hello é iniciado, insira o alias de saudação do usuário Olá desejar toolook e clique em botão de saudação.</span><span class="sxs-lookup"><span data-stu-id="77d89-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="77d89-223">Será solicitada a sua autenticação.</span><span class="sxs-lookup"><span data-stu-id="77d89-223">You're prompted for authentication.</span></span> <span data-ttu-id="77d89-224">Após a autenticação bem-sucedida e pesquisa bem-sucedida, atributos de saudação do usuário Olá pesquisado são exibidos.</span><span class="sxs-lookup"><span data-stu-id="77d89-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="77d89-225">As execuções subsequentes executará Olá pesquisa sem mostrar qualquer prompt, graças toohello presença Olá anteriormente adquirido token em cache.</span><span class="sxs-lookup"><span data-stu-id="77d89-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="77d89-226">etapas de concreto Olá para executar o aplicativo hello variam por plataforma.</span><span class="sxs-lookup"><span data-stu-id="77d89-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="77d89-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="77d89-227">Windows 10</span></span>
   <span data-ttu-id="77d89-228">Tablet/computador: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="77d89-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="77d89-229">Dispositivos móveis (requer um dispositivo conectado de Windows 10 Mobile tooa PC):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="77d89-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="77d89-230">Durante a saudação executado pela primeira vez, você pode ser solicitado toosign em uma licença de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="77d89-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="77d89-231">Para mais informações, consulte [Licença de desenvolvedor](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="77d89-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="77d89-232">Tablet/computador Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="77d89-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="77d89-233">Durante a saudação executado pela primeira vez, você pode ser solicitado toosign em uma licença de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="77d89-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="77d89-234">Para mais informações, consulte [Licença de desenvolvedor](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="77d89-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="77d89-235">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="77d89-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="77d89-236">toorun em um dispositivo conectado:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="77d89-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="77d89-237">toorun no emulador do saudação padrão:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="77d89-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="77d89-238">Use `cordova run windows --list -- --phone` toosee todos os destinos disponíveis e `cordova run windows --target=<target_name> -- --phone` toorun aplicativo de hello em um determinado dispositivo ou emulador (por exemplo, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="77d89-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="77d89-239">Android</span><span class="sxs-lookup"><span data-stu-id="77d89-239">Android</span></span>
   <span data-ttu-id="77d89-240">toorun em um dispositivo conectado:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="77d89-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="77d89-241">toorun no emulador do saudação padrão:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="77d89-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="77d89-242">Verifique se que você criou uma instância do emulador usando o Gerenciador de AVD, conforme descrito anteriormente na seção "Pré-requisitos" de saudação.</span><span class="sxs-lookup"><span data-stu-id="77d89-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="77d89-243">Use `cordova run android --list` toosee todos os destinos disponíveis e `cordova run android --target=<target_name>` toorun aplicativo de hello em um determinado dispositivo ou emulador (por exemplo, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="77d89-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="77d89-244">iOS</span><span class="sxs-lookup"><span data-stu-id="77d89-244">iOS</span></span>
   <span data-ttu-id="77d89-245">toorun em um dispositivo conectado:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="77d89-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="77d89-246">toorun no emulador do saudação padrão:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="77d89-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="77d89-247">Verifique se você tem Olá `ios-sim` toorun pacote instalado no emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="77d89-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="77d89-248">Para obter mais informações, consulte hello "pré-requisitos" seção.</span><span class="sxs-lookup"><span data-stu-id="77d89-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="77d89-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77d89-249">Next steps</span></span>
<span data-ttu-id="77d89-250">Para referência, o exemplo hello concluída (sem os valores de configuração) está disponível em [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="77d89-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="77d89-251">Você pode agora cenários de movimentação em toomore avançado (e mais interessante).</span><span class="sxs-lookup"><span data-stu-id="77d89-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="77d89-252">Talvez você queira tootry: [proteger uma API da Web Node. js com o Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="77d89-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
