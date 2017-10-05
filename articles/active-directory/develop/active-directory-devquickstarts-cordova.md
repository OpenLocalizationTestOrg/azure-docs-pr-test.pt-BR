---
title: "Introdução a Cordova no AD do Azure | Microsoft Docs"
description: Como compilar um aplicativo do Cordova que se integra ao Azure AD para entrada e que chama APIs protegidas do Azure AD usando OAuth.
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
ms.openlocfilehash: d9f53148787729d29a0a89cce1b8b2b83ba228f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="ab5ec-103">Integrar o AD do Azure com um aplicativo Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="ab5ec-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ab5ec-104">Você pode usar o Apache Cordova para desenvolver aplicativos HTML5/JavaScript que podem ser executados em dispositivos móveis, como aplicativos nativos completos.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="ab5ec-105">Com o Azure Active Directory (Azure AD), você pode adicionar recursos de autenticação de nível empresarial a seus aplicativos Cordova.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="ab5ec-106">Um plug-in do Cordova encapsula os SDKs nativos do Azure AD em iOS, Android, Windows Store e Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="ab5ec-107">Usando esse plug-in, você pode aprimorar seu aplicativo para dar suporte à entrada com contas do Active Directory do Windows Server de seus usuários, obter acesso ao Office 365 e APIs do Azure e até mesmo ajudar a proteger chamadas para sua própria API da web personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="ab5ec-108">Neste tutorial, usaremos o plug-in do Apache Cordova para a Biblioteca de Autenticação do Active Directory (ADAL) para aprimorar um aplicativo simples adicionando os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="ab5ec-109">Com apenas algumas linhas de código, autenticar um usuário e obter um token.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="ab5ec-110">Usar esse token para invocar a API do Graph para consultar o diretório e exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="ab5ec-111">Use o cache de token da ADAL para minimizar os prompts de autenticação para o usuário.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="ab5ec-112">Para fazer essas melhorias, você precisa:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="ab5ec-113">Registrar um aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="ab5ec-114">Adicione código ao seu aplicativo para solicitar tokens.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="ab5ec-115">Adicionar código para usar o token para consultar a Graph API e exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="ab5ec-116">Criar o projeto de implantação Cordova com todas as plataformas de destino, adicionar o plug-in Cordova ADAL e testar a solução em emuladores.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab5ec-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ab5ec-117">Prerequisites</span></span>
<span data-ttu-id="ab5ec-118">Para concluir este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="ab5ec-119">Um locatário do Azure AD onde você pode ter uma conta com direitos de desenvolvimento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="ab5ec-120">Um ambiente de desenvolvimento configurado para usar o Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="ab5ec-121">Se você já tiver ambos configurados, vá diretamente para a etapa 1.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="ab5ec-122">Se você não tiver um locatário do Azure AD, use as [instruções sobre como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="ab5ec-123">Se você não tiver o Apache Cordova configurado no seu computador, instale o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="ab5ec-124">Git</span><span class="sxs-lookup"><span data-stu-id="ab5ec-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="ab5ec-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="ab5ec-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="ab5ec-126">[Cordova CLI](https://cordova.apache.org/) (pode ser facilmente instalado por meio do gerenciador de pacotes NPM: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="ab5ec-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="ab5ec-127">As instalações anteriores devem funcionar no PC e no Mac.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="ab5ec-128">Cada plataforma de destino tem pré-requisitos diferentes:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="ab5ec-129">Para compilar e executar um aplicativo para Tablet/PC Windows ou Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="ab5ec-130">Instale o [Visual Studio 2013 para Windows com Atualização 2 ou superior](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express ou outra versão) ou [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="ab5ec-131">Para compilar e executar um aplicativo para iOS:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="ab5ec-132">Instale o Xcode 6.x ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="ab5ec-133">Baixe-o no [site de desenvolvedores da Apple](http://developer.apple.com/downloads) ou na [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="ab5ec-134">Instale o [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="ab5ec-135">Você pode usá-lo para iniciar aplicativos iOS no simulador do iOS na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="ab5ec-136">(Você pode instalá-lo facilmente por meio do terminal: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="ab5ec-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="ab5ec-137">Para compilar e executar um aplicativo para Android:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="ab5ec-138">Instale [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="ab5ec-139">Certifique-se de que `JAVA_HOME` (variável de ambiente) está configurado corretamente de acordo com o caminho de instalação do JDK (por exemplo C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="ab5ec-140">Instale o [SDK do Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) e adicione o local `<android-sdk-location>\tools` (por exemplo, C:\tools\Android\android-sdk\tools) em sua `PATH` variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="ab5ec-141">Abra o Gerenciador de SDK do Android (por exemplo, por meio do terminal: `android`) e instale:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="ab5ec-142">*Android 5.0.1 (API 21)* SDK de plataforma</span><span class="sxs-lookup"><span data-stu-id="ab5ec-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="ab5ec-143">*Android SDK Build-tools* versão 19.1.0 ou superior</span><span class="sxs-lookup"><span data-stu-id="ab5ec-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="ab5ec-144">*Repositório de suporte do Android* (Extras)</span><span class="sxs-lookup"><span data-stu-id="ab5ec-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="ab5ec-145">O SDK do Android não fornece qualquer instância do emulador padrão.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="ab5ec-146">Crie uma nova executando `android avd` no terminal e, em seguida, selecionando **Criar**, se você quiser executar o aplicativo Android em um emulador.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="ab5ec-147">Recomendamos um nível de API de 19 ou superior.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="ab5ec-148">Para obter mais informações sobre as opções de criação e o emulador Android, consulte [Gerenciador AVD](http://developer.android.com/tools/help/avd-manager.html) no site do Android.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="ab5ec-149">Etapa 1: registrar um aplicativo com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab5ec-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="ab5ec-150">Esta etapa é opcional.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-150">This step is optional.</span></span> <span data-ttu-id="ab5ec-151">Este tutorial fornece valores previamente provisionados que você pode usar para ver o exemplo em ação sem fazer nenhum provisionamento em seu próprio locatário.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="ab5ec-152">No entanto, é recomendável que você execute essa etapa e se familiarize com o processo, pois ele será necessário quando você criar seus próprios aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="ab5ec-153">O Azure AD emite tokens somente para aplicativos conhecidos.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="ab5ec-154">Antes de poder usar o AD do Azure do seu aplicativo, você precisa criar uma entrada para ele no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="ab5ec-155">Para registrar um novo aplicativo no seu locatário:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="ab5ec-156">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ab5ec-157">Na barra superior, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-157">On the top bar, click your account.</span></span> <span data-ttu-id="ab5ec-158">Na lista **Diretório**, escolha o locatário do Azure AD no qual você quer registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="ab5ec-159">Clique em **Mais Serviços** no painel esquerdo e selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ab5ec-160">Clique em **Registros do aplicativo**e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="ab5ec-161">Siga os prompts e crie um **Aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="ab5ec-162">(Embora os aplicativos Cordova sejam baseados em HTML, estamos criando um aplicativo cliente nativo aqui.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="ab5ec-163">A opção **Aplicativo cliente nativo** deve ser selecionada, ou o aplicativo não funcionará).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="ab5ec-164">**Nome** descreve seu aplicativo para os usuários.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="ab5ec-165">**URI de Redirecionamento** é o URI usado para retornar os tokens para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="ab5ec-166">Digite **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="ab5ec-167">Depois de concluir o registro, o Azure AD atribui uma identificação exclusiva do aplicativo ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="ab5ec-168">Você precisará desse valor nas próximas seções.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="ab5ec-169">Você o encontrará na guia do aplicativo do aplicativo recém-criado.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="ab5ec-170">Para executar `DirSearchClient Sample`, dê permissão ao aplicativo recém-criado para consultar a API do Graph do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="ab5ec-171">Na página **Configurações**, selecione **Permissões necessárias** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="ab5ec-172">Para o aplicativo Azure Active Directory, selecione **Microsoft Graph** como a API e adicione a permissão **Acessar o diretório como o usuário conectado** em **Permissões delegadas**.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="ab5ec-173">Isso permite que seu aplicativo consulte a API do Graph para usuários.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="ab5ec-174">Etapa 2: clonar o repositório do aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="ab5ec-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="ab5ec-175">No shell ou na linha de comando, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="ab5ec-176">Etapa 3: criar o aplicativo Cordova</span><span class="sxs-lookup"><span data-stu-id="ab5ec-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="ab5ec-177">Há várias maneiras de criar aplicativos Cordova.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="ab5ec-178">Neste tutorial, usaremos a interface de linha de comando do Cordova (CLI).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="ab5ec-179">No shell ou na linha de comando, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="ab5ec-180">O comando cria a estrutura de pastas e scaffolding para o projeto Cordova.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="ab5ec-181">Siga para a nova pasta DirSearchClient:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="ab5ec-182">Copie o conteúdo do projeto inicial na subpasta www usando um gerenciador de arquivos ou o seguinte comando no seu shell:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="ab5ec-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="ab5ec-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="ab5ec-185">Adicione a lista branca de plug-in.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="ab5ec-186">Isso é necessário para invocar a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="ab5ec-187">Adicione todas as plataformas às quais deseja oferecer suporte.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="ab5ec-188">Para obter um exemplo funcional, você precisará executar pelo menos um dos comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="ab5ec-189">Observe que você não poderá emular o iOS no Windows ou emular o Windows em um Mac.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="ab5ec-190">Adicione a ADAL para o plug-in Cordova no seu projeto:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="ab5ec-191">Etapa 4: adicionar código para autenticar usuários e obter tokens do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab5ec-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="ab5ec-192">O aplicativo que você está desenvolvendo neste tutorial fornecerá um recurso de pesquisa de diretório simples.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="ab5ec-193">O usuário poderá, então, digitar o alias de qualquer usuário no diretório e visualizar alguns atributos básicos.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="ab5ec-194">O projeto inicial contém a definição da interface do usuário básico do aplicativo (em www/index.html) e o scaffolding que conecta os ciclos de eventos do aplicativo básico, ligações de interface do usuário e a lógica de exibição dos resultados (em www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="ab5ec-195">A única tarefa que falta para você fazer é adicionar a lógica que implementa as tarefas de identidade.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="ab5ec-196">A primeira coisa que você precisa fazer no seu código é apresentar os valores de protocolo que o Azure AD usa para identificar o seu aplicativo e os recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="ab5ec-197">Esses valores serão usados para construir as solicitações de token posteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="ab5ec-198">Insira o trecho a seguir na parte superior do arquivo index.js:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="ab5ec-199">Os valores `redirectUri` e `clientId` devem corresponder aos valores que descrevem o seu aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="ab5ec-200">Você pode encontrá-los na guia **Configurar** no portal do Azure, conforme descrito na etapa 1, mostrada anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="ab5ec-201">Se tiver optado por não registrar um novo aplicativo no seu próprio locatário, você pode simplesmente colar os valores pré-configurados como tal.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="ab5ec-202">Você poderá ver o exemplo em execução, embora sempre deva criar sua própria entrada para os aplicativos destinados a produção.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="ab5ec-203">Em seguida, adicione o código de solicitação de token.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-203">Next, add the token request code.</span></span> <span data-ttu-id="ab5ec-204">Insira o trecho a seguir entre as definições `search` e `renderData`:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="ab5ec-205">Vamos examinar essa função, separando-a em suas duas partes principais.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="ab5ec-206">Esse exemplo foi criado para funcionar com qualquer locatário, em vez de estar vinculado a um locatário determinado.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="ab5ec-207">Ele usa o ponto de extremidade "/common", que permite que o usuário insira qualquer conta no momento da autenticação e direciona a solicitação para o locatário a que ela pertence.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="ab5ec-208">Esta primeira parte do método inspeciona o cache da ADAL para ver se um token já está armazenado.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="ab5ec-209">Nesse caso, o método usa os locatários de onde o token veio para reinicializar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="ab5ec-210">Isso é necessário para evitar prompts extras, uma vez que o uso de "/common" sempre resulta em solicitar que o usuário insira uma nova conta.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="ab5ec-211">A segunda parte do método executa a solicitação de token adequada.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="ab5ec-212">O método `acquireTokenSilentAsync` solicita que a ADAL retorne um token para o recurso especificado sem mostrar qualquer experiência do usuário.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="ab5ec-213">Isso pode acontecer se o cache já tiver um token de acesso adequado armazenado, ou se houver um token de atualização que pode ser usado para obter um novo token de acesso sem mostrar nenhum prompt.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="ab5ec-214">Se essa tentativa falhar, voltamos para `acquireTokenAsync`, que solicitará visivelmente que o usuário seja autenticado.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="ab5ec-215">Agora que temos o token, podemos finalmente invocar a API do Graph e executar a consulta de pesquisa desejada.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="ab5ec-216">Insira o trecho a seguir logo abaixo da definição `authenticate`:</span><span class="sxs-lookup"><span data-stu-id="ab5ec-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
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
<span data-ttu-id="ab5ec-217">Os arquivos de ponto de partida forneceram uma experiência do usuário simples para digitar o alias de um usuário em uma caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="ab5ec-218">Esse método usa esse valor para construir uma consulta, combiná-la ao token de acesso, enviá-la ao Microsoft Graph e analisar os resultados.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="ab5ec-219">O método `renderData`, já presente no arquivo de ponto de partida, se encarrega de visualizar os resultados.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="ab5ec-220">Etapa 5: executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="ab5ec-220">Step 5: Run the app</span></span>
<span data-ttu-id="ab5ec-221">Seu aplicativo está finalmente pronto para execução.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-221">Your app is finally ready to run.</span></span> <span data-ttu-id="ab5ec-222">Operá-lo é simples: quando o aplicativo for iniciado, digite na caixa de texto o alias do usuário que você deseja pesquisar e clique no botão.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="ab5ec-223">Será solicitada a sua autenticação.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-223">You're prompted for authentication.</span></span> <span data-ttu-id="ab5ec-224">Após a autenticação e pesquisa bem-sucedidas, os atributos do usuário pesquisado serão exibidos.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="ab5ec-225">Execuções subsequentes executarão a pesquisa sem mostrar qualquer prompt, devido à presença do token adquirido anteriormente em cache.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="ab5ec-226">As etapas concretas para execução do aplicativo variam de acordo com a plataforma.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="ab5ec-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="ab5ec-227">Windows 10</span></span>
   <span data-ttu-id="ab5ec-228">Tablet/computador: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="ab5ec-229">Dispositivo móvel (requer um dispositivo móvel do Windows10 conectado a um computador): `cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="ab5ec-230">Durante a primeira execução, pode ser solicitado que você se inscreva para uma licença de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="ab5ec-231">Para mais informações, consulte [Licença de desenvolvedor](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="ab5ec-232">Tablet/computador Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ab5ec-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="ab5ec-233">Durante a primeira execução, pode ser solicitado que você se inscreva para uma licença de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="ab5ec-234">Para mais informações, consulte [Licença de desenvolvedor](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="ab5ec-235">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="ab5ec-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="ab5ec-236">Para executar em um dispositivo conectado: `cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="ab5ec-237">Para executar no emulador padrão: `cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="ab5ec-238">Use `cordova run windows --list -- --phone` para ver todos os destinos disponíveis e `cordova run windows --target=<target_name> -- --phone` para executar o aplicativo em um emulador ou dispositivo específico (por exemplo, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="ab5ec-239">Android</span><span class="sxs-lookup"><span data-stu-id="ab5ec-239">Android</span></span>
   <span data-ttu-id="ab5ec-240">Para executar em um dispositivo conectado: `cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="ab5ec-241">Para executar no emulador padrão: `cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="ab5ec-242">Verifique se que você criou uma instância do emulador usando o Gerenciador de AVD, conforme descrito anteriormente na seção "Pré-requisitos".</span><span class="sxs-lookup"><span data-stu-id="ab5ec-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="ab5ec-243">Use `cordova run android --list` para ver todos os destinos disponíveis e `cordova run android --target=<target_name>` para executar o aplicativo em um emulador ou dispositivo específico (por exemplo, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="ab5ec-244">iOS</span><span class="sxs-lookup"><span data-stu-id="ab5ec-244">iOS</span></span>
   <span data-ttu-id="ab5ec-245">Para executar em um dispositivo conectado: `cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="ab5ec-246">Para executar no emulador padrão: `cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="ab5ec-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="ab5ec-247">Verifique se você tem o pacote `ios-sim` instalado para ser executado no emulador.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="ab5ec-248">Para mais informações, consulte a seção “Pré-requisitos”.</span><span class="sxs-lookup"><span data-stu-id="ab5ec-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="ab5ec-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab5ec-249">Next steps</span></span>
<span data-ttu-id="ab5ec-250">Para referência, o exemplo concluído (sem seus valores de configuração) está disponível no [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="ab5ec-251">Agora você pode passar para cenários mais avançados (e mais interessantes).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="ab5ec-252">Você talvez queira: [proteger uma API da Web Node. js com o Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ab5ec-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
