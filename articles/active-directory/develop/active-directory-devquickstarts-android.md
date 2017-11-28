---
title: "aaaAzure AD Android Introdução | Microsoft Docs"
description: Como toobuild um aplicativo do Android que se integra ao AD do Azure para entrar e chamadas de AD do Azure APIs protegidas usando OAuth.
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="e6fcb-103">Integração do Azure AD a um aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="e6fcb-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="e6fcb-104">Experimentar a visualização de saudação do nosso novo [portal do desenvolvedor](https://identity.microsoft.com/Docs/Android), que irá ajudá-lo a colocar em funcionamento com o Azure AD em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="e6fcb-105">portal do desenvolvedor Olá irá orientá-lo pelo processo de saudação do registro de um aplicativo e a integração do AD do Azure em seu código.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="e6fcb-106">Quando terminar, você terá um aplicativo simples que pode autenticar os usuários em seu locatário e um back-end que pode aceitar tokens e executar a validação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="e6fcb-107">Se você estiver desenvolvendo um aplicativo de desktop, Azure Active Directory (AD do Azure) torna simples e direta para você tooauthenticate os usuários com suas contas do Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="e6fcb-108">Ele também permite que seu aplicativo toosecurely consumir qualquer web API protegida pelo AD do Azure, como Olá APIs do Office 365 ou Olá API do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="e6fcb-109">Para clientes do Android que necessitam de recursos tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="e6fcb-110">Olá única finalidade ADAL é toomake fácil para seus tokens de acesso do aplicativo tooget.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="e6fcb-111">toodemonstrate fácil é, criaremos um aplicativo do Android lista de tarefas que:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="e6fcb-112">Obtém acesso tokens para chamar uma API da lista de tarefas usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="e6fcb-113">Obtém a lista de tarefas pendentes de um usuário.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="e6fcb-114">Desconecta usuários.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-114">Signs out users.</span></span>

<span data-ttu-id="e6fcb-115">tooget iniciado, você precisa de um locatário do AD do Azure, na qual você pode criar usuários e registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="e6fcb-116">Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="e6fcb-117">Etapa 1: Baixar e executar o servidor de exemplo hello Node. js REST API TODO</span><span class="sxs-lookup"><span data-stu-id="e6fcb-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="e6fcb-118">exemplo de Node. js REST API TODO Hello é gravado especificamente toowork em nosso exemplo existente para a criação de um API de REST de tarefas pendentes de único locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="e6fcb-119">Este é um pré-requisito para Olá início rápido.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="e6fcb-120">Para obter informações sobre como tooset isso, consulte nossos exemplos existentes em [Microsoft Azure exemplo REST API de serviço do Active Directory para Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="e6fcb-121">Etapa 2: Registre sua API da Web com seu locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6fcb-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="e6fcb-122">O Active Directory dá suporte à adição de dois tipos de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="e6fcb-123">APIs da Web que oferecem serviços toousers</span><span class="sxs-lookup"><span data-stu-id="e6fcb-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="e6fcb-124">Aplicativos (executando em Olá web ou em um dispositivo) que acessam as APIs de web</span><span class="sxs-lookup"><span data-stu-id="e6fcb-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="e6fcb-125">Nesta etapa, você está registrando Olá web API que você está executando localmente para testar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="e6fcb-126">Normalmente, essa API da web é um serviço REST que é a funcionalidade de oferta que você deseja que um aplicativo tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="e6fcb-127">O Azure AD pode ajudar a proteger qualquer ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="e6fcb-128">Estamos supondo que você está registrando Olá TODO REST API mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="e6fcb-129">Mas isso funciona para qualquer API da web que você deseja proteger toohelp Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="e6fcb-130">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e6fcb-131">Na barra superior do hello, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-131">On hello top bar, click your account.</span></span> <span data-ttu-id="e6fcb-132">Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="e6fcb-133">Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e6fcb-134">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e6fcb-135">Insira um nome amigável para o aplicativo hello (por exemplo, **TodoListService**), selecione **aplicativo Web e/ou API da Web**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="e6fcb-136">Para Olá URL de logon, insira a URL base Olá para exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="e6fcb-137">Por padrão, ela é `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="e6fcb-138">Clique em **Okey** toocomplete registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="e6fcb-139">Ainda no hello portal do Azure, acesse a página de aplicativo tooyour, localizar o valor de ID de aplicativo hello e copiá-lo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="e6fcb-140">Você precisará dele mais tarde ao configurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="e6fcb-141">De saudação **configurações** -> **propriedades** página, atualize o URI da ID do aplicativo hello - digite `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="e6fcb-142">Substituir `<your_tenant_name>` com nome de saudação do seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="e6fcb-143">Etapa 3: Registrar o aplicativo de Android Native Client do exemplo hello</span><span class="sxs-lookup"><span data-stu-id="e6fcb-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="e6fcb-144">Registre seu aplicativo da Web neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-144">You must register your web application in this sample.</span></span> <span data-ttu-id="e6fcb-145">Isso permite que toocommunicate seu aplicativo com hello registrados apenas API da web.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="e6fcb-146">O AD do Azure recusará tooeven permitir tooask seu aplicativo para entrar, a menos que ele está registrado.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="e6fcb-147">Que faz parte da segurança de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="e6fcb-148">Estamos supondo que você está registrando o aplicativo de exemplo hello mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="e6fcb-149">Porém, este procedimento funciona para qualquer aplicativo que você esteja desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="e6fcb-150">Talvez você se pergunte por que está colocando um aplicativo e uma API da Web em um locatário.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="e6fcb-151">Como você deve ter adivinhado, é possível compilar um aplicativo que acessa uma API externa que é registrada no Azure AD de outro locatário.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="e6fcb-152">Se você fizer isso, os clientes serão solicitados tooconsent toohello uso Olá API no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="e6fcb-153">A biblioteca de autenticação do Active Directory para iOS se encarrega desse consentimento por você.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="e6fcb-154">Como podemos explorar recursos mais avançados, você verá que se trata de uma parte importante do conjunto de saudação do hello trabalho tooaccess necessárias de APIs do Office e do Azure, bem como qualquer outro provedor de serviço do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="e6fcb-155">Por enquanto, como você se registrou sua API da web e o aplicativo hello mesmo locatário, você não verá quaisquer solicitações de consentimento.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="e6fcb-156">Isso geralmente é o caso de Olá se você estiver desenvolvendo um aplicativo apenas para seu próprio toouse da empresa.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="e6fcb-157">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e6fcb-158">Na barra superior do hello, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-158">On hello top bar, click your account.</span></span> <span data-ttu-id="e6fcb-159">Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="e6fcb-160">Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e6fcb-161">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e6fcb-162">Insira um nome amigável para o aplicativo hello (por exemplo, **TodoListClient Android**), selecione **aplicativo cliente nativo**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="e6fcb-163">URI de redirecionamento para hello, digite `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="e6fcb-164">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-164">Click **Finish**.</span></span>
7. <span data-ttu-id="e6fcb-165">Na página de aplicativo hello, localizar o valor de ID de aplicativo hello e copiá-lo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="e6fcb-166">Você precisará dele mais tarde ao configurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="e6fcb-167">De saudação **configurações** página, selecione **permissões necessárias** e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="e6fcb-168">Localize e selecione TodoListService, adicionar Olá **acesso TodoListService** permissão em **permissões delegadas**e clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="e6fcb-169">toobuild com o Maven, você pode usar pom.xml no nível superior da saudação:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="e6fcb-170">Clone esse repositório em um diretório de sua escolha:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="e6fcb-171">Siga as etapas de Olá Olá [tooset pré-requisitos seu ambiente Maven para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="e6fcb-172">Configure o emulador Olá 19 SDK.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="e6fcb-173">Acesse a pasta raiz de toohello onde você clonou repositório hello.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="e6fcb-174">Execute este comando: `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="e6fcb-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="e6fcb-175">Alterar o exemplo de início rápido do hello diretório toohello:`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="e6fcb-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="e6fcb-176">Execute este comando: `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="e6fcb-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="e6fcb-177">Você deve ver a saudação inicial de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="e6fcb-178">Insira tootry de credenciais de usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="e6fcb-179">JAR pacotes serão enviados ao lado do pacote do hello AAR.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="e6fcb-180">Etapa 4: Baixar Olá Android ADAL e adicioná-lo tooyour espaço de trabalho do Eclipse</span><span class="sxs-lookup"><span data-stu-id="e6fcb-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="e6fcb-181">Tornamos fácil para você toohave várias opções toouse ADAL em seu projeto Android:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="e6fcb-182">Você pode usar o hello tooimport de código de origem nesta biblioteca no aplicativo de tooyour Eclipse e link.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="e6fcb-183">Se você estiver usando o Android Studio, você pode usar o hello AAR pacote referência e formato Olá binários.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="e6fcb-184">Opção 1: zip de origem</span><span class="sxs-lookup"><span data-stu-id="e6fcb-184">Option 1: Source Zip</span></span>
<span data-ttu-id="e6fcb-185">toodownload uma cópia do código-fonte hello, clique em **baixar ZIP** Olá direita da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="e6fcb-186">Ou [baixe do GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="e6fcb-187">Opção 2: Origem via Git</span><span class="sxs-lookup"><span data-stu-id="e6fcb-187">Option 2: Source via Git</span></span>
<span data-ttu-id="e6fcb-188">código-fonte tooget saudação do hello SDK por meio de Git, digite:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="e6fcb-189">Opção 3: Binários via Gradle</span><span class="sxs-lookup"><span data-stu-id="e6fcb-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="e6fcb-190">Você pode obter os binários de saudação do repositório central de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="e6fcb-191">pacote de AAR Olá pode ser incluído em seu projeto no Android Studio da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="e6fcb-192">Opção 4: AAR via Maven</span><span class="sxs-lookup"><span data-stu-id="e6fcb-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="e6fcb-193">Se você estiver usando Olá M2Eclipse plug-in, você pode especificar a dependência de saudação em seu arquivo pom.xml:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="e6fcb-194">Opção 5: Pacote JAR dentro da pasta de bibliotecas de saudação</span><span class="sxs-lookup"><span data-stu-id="e6fcb-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="e6fcb-195">Você pode obter o arquivo JAR de saudação do repositório de Maven hello e inseri-la em Olá **bibliotecas** pasta em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="e6fcb-196">Você precisa toocopy Olá recursos necessários tooyour projeto, porque os pacotes JAR Olá não incluem-los.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="e6fcb-197">Etapa 5: Adicionar um projeto ADAL tooyour tooAndroid referências</span><span class="sxs-lookup"><span data-stu-id="e6fcb-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="e6fcb-198">Adicione uma referência de projeto do tooyour e especificá-la como uma biblioteca Android.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="e6fcb-199">Se não tiver certeza como toodo isso, você pode obter mais informações sobre Olá [site Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="e6fcb-200">Adicione dependência de projeto Olá para depuração em suas configurações de projeto.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="e6fcb-201">Atualize tooinclude de arquivo AndroidManifest.xml do projeto:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="e6fcb-202">Crie uma instância de AuthenticationContext na atividade principal.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="e6fcb-203">Olá detalhes desta chamada além do escopo deste tópico hello, mas você pode obter um bom começo examinando Olá [exemplo do Android Native Client](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="e6fcb-204">Em Olá exemplo a seguir, SharedPreferences é cache padrão de saudação e autoridade está na forma de saudação do `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="e6fcb-205">Copie esta final do código bloco toohandle Olá de AuthenticationActivity depois insere as credenciais de usuário de saudação e recebe um código de autorização:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="e6fcb-206">tooask para um token, defina um retorno de chamada:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-206">tooask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="e6fcb-207">Por fim, solicite um token usando esse retorno de chamada:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="e6fcb-208">Aqui está uma explicação sobre os parâmetros de saudação:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="e6fcb-209">*recurso* é necessária e recurso Olá estiver tentando tooaccess.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="e6fcb-210">*clientid* é obrigatório e é proveniente do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="e6fcb-211">*RedirectUri* não é necessário toobe fornecido para a chamada de acquireToken hello.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="e6fcb-212">Configure-o como o nome de seu pacote.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="e6fcb-213">*PromptBehavior* ajuda tooask para cache de saudação tooskip credenciais e o cookie.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="e6fcb-214">*retorno de chamada* é chamado depois que o código de autorização de saudação é trocado por um token.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="e6fcb-215">Ele possui um objeto AuthenticationResult, que tem informações sobre o token de acesso, a data de vencimento e o token de ID.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="e6fcb-216">*acquireTokenSilent* é opcional.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="e6fcb-217">Você pode chamá-lo toohandle cache e atualização do token.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="e6fcb-218">Ele também fornece a versão de sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-218">It also provides hello sync version.</span></span> <span data-ttu-id="e6fcb-219">Ele aceita *userid* como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="e6fcb-220">Usando este passo a passo, você deve ter o que você precisa toosuccessfully integrar com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="e6fcb-221">Para obter mais exemplos disso funcionar, visite Olá AzureADSamples / repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="e6fcb-222">Informações importantes</span><span class="sxs-lookup"><span data-stu-id="e6fcb-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="e6fcb-223">Personalização</span><span class="sxs-lookup"><span data-stu-id="e6fcb-223">Customization</span></span>
<span data-ttu-id="e6fcb-224">Os recursos de seu aplicativo podem substituir os recursos de projeto da biblioteca.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="e6fcb-225">Isso acontece quando seu aplicativo está sendo compilado.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-225">This happens when your app is being built.</span></span> <span data-ttu-id="e6fcb-226">Por esse motivo, você pode personalizar o modo de saudação do autenticação atividade layout desejado.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="e6fcb-227">ID de Olá tookeep-se de controles de saudação que ADAL usa (exibição da Web).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="e6fcb-228">Agente</span><span class="sxs-lookup"><span data-stu-id="e6fcb-228">Broker</span></span>
<span data-ttu-id="e6fcb-229">aplicativo de Portal da empresa do Microsoft Intune Olá fornece o componente de agente do hello.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="e6fcb-230">Olá conta é criada no AccountManager.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="e6fcb-231">tipo de conta de saudação é "workaccount".</span><span class="sxs-lookup"><span data-stu-id="e6fcb-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="e6fcb-232">AccountManager permite apenas uma única conta SSO.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="e6fcb-233">Ele cria um cookie SSO para o usuário Olá depois de concluir o desafio de dispositivo Olá para um dos aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="e6fcb-234">ADAL usa a conta de agente de saudação se uma conta de usuário é criada nesse autenticador e você escolher não tooskip-lo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="e6fcb-235">Você pode ignorar o usuário de agente Olá com:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="e6fcb-236">Você precisa tooregister um RedirectUri especial para uso do agente.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="e6fcb-237">RedirectUri está no formato de saudação do `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="e6fcb-238">Você pode obter o RedirectUri para seu aplicativo usando Olá script brokerRedirectPrint.ps1 ou Olá API chamada mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="e6fcb-239">assinatura de saudação é tooyour relacionado certificados de assinatura.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="e6fcb-240">modelo de broker atual Olá é para um usuário.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-240">hello current broker model is for one user.</span></span> <span data-ttu-id="e6fcb-241">AuthenticationContext fornece um usuário de agente de Olá Olá API método tooget.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="e6fcb-242">O manifesto do aplicativo deve ter Olá contas de AccountManager toouse permissões a seguir.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="e6fcb-243">Para obter detalhes, consulte Olá [AccountManager informações no site Android Olá](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="e6fcb-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="e6fcb-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="e6fcb-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="e6fcb-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="e6fcb-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="e6fcb-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="e6fcb-247">URL da Autoridade e AD FS</span><span class="sxs-lookup"><span data-stu-id="e6fcb-247">Authority URL and AD FS</span></span>
<span data-ttu-id="e6fcb-248">Os serviços de Federação do Active Directory (AD FS) não é reconhecido como produção STS, para que você precisa tooturn de descoberta da instância e passe false no construtor de AuthenticationContext hello.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="e6fcb-249">Olá autoridade URL precisa de uma instância de STS e um [nome do locatário](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="e6fcb-250">Consultar itens do cache</span><span class="sxs-lookup"><span data-stu-id="e6fcb-250">Querying cache items</span></span>
<span data-ttu-id="e6fcb-251">A ADAL fornece um cache padrão em SharedPreferences com algumas funções de consulta de cache simples.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="e6fcb-252">Você pode obter cache atual de saudação do AuthenticationContext usando:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="e6fcb-253">Você também pode fornecer a implementação do cache, se você quiser toocustomize-lo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="e6fcb-254">Comportamento da solicitação</span><span class="sxs-lookup"><span data-stu-id="e6fcb-254">Prompt behavior</span></span>
<span data-ttu-id="e6fcb-255">O ADAL fornece um comportamento do prompt toospecify opção.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="e6fcb-256">PromptBehavior.Auto mostrará a saudação da interface do usuário se o token de atualização de saudação é inválido e são necessárias credenciais de usuário.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="e6fcb-257">PromptBehavior.Always irá ignorar o uso de cache de saudação e sempre mostrar Olá da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="e6fcb-258">Solicitação de token silenciosa do cache e atualização</span><span class="sxs-lookup"><span data-stu-id="e6fcb-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="e6fcb-259">Uma solicitação de token silenciosa não usa Olá pop-up de interface do usuário e não requer uma atividade.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="e6fcb-260">Ele retorna um token de cache hello, se disponível.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="e6fcb-261">Se o token Olá tiver expirado, esse método tentará toorefresh-lo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="e6fcb-262">Se o token de atualização de saudação expirou ou falha, ele retornará AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="e6fcb-263">Você também pode fazer uma chamada de sincronização com esse método.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="e6fcb-264">Você pode definir toocallback nulo ou use acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="e6fcb-265">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="e6fcb-265">Diagnostics</span></span>
<span data-ttu-id="e6fcb-266">Estas são as Olá principais fontes de informações para diagnosticar problemas:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="e6fcb-267">Exceções</span><span class="sxs-lookup"><span data-stu-id="e6fcb-267">Exceptions</span></span>
* <span data-ttu-id="e6fcb-268">Logs</span><span class="sxs-lookup"><span data-stu-id="e6fcb-268">Logs</span></span>
* <span data-ttu-id="e6fcb-269">Rastreamentos de rede</span><span class="sxs-lookup"><span data-stu-id="e6fcb-269">Network traces</span></span>

<span data-ttu-id="e6fcb-270">Observe que as IDs de correlação são diagnóstico toohello central na biblioteca de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="e6fcb-271">Você pode definir suas IDs de correlação em uma base por solicitação, se você quiser toocorrelate solicitar uma ADAL com outras operações em seu código.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="e6fcb-272">Se você não definir uma ID de correlação, a ADAL gerará uma senha aleatória.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="e6fcb-273">Todas as mensagens de log e, em seguida, chamadas de rede serão carimbadas com ID de correlação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="e6fcb-274">Olá gerado automaticamente ID as alterações em cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="e6fcb-275">Exceções</span><span class="sxs-lookup"><span data-stu-id="e6fcb-275">Exceptions</span></span>
<span data-ttu-id="e6fcb-276">Exceções são Olá primeiro diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="e6fcb-277">Tentamos tooprovide mensagens de erro úteis.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="e6fcb-278">Se você encontrar uma que não é útil, registre um problema e nos informe.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="e6fcb-279">Inclua informações do dispositivo, como modelo e número do SDK.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="e6fcb-280">Logs</span><span class="sxs-lookup"><span data-stu-id="e6fcb-280">Logs</span></span>
<span data-ttu-id="e6fcb-281">Você pode configurar Olá biblioteca toogenerate mensagens de log que você pode usar toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="e6fcb-282">Configurar o log fazendo o seguinte Olá chamar tooconfigure um retorno de chamada que ADAL usará toohand cada mensagem de log gerado.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="e6fcb-283">As mensagens podem ser gravadas tooa o arquivo de log personalizado, como mostrado na saudação de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="e6fcb-284">Infelizmente, não há um modo padrão de obter os logs de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="e6fcb-285">Há alguns serviços que podem ajudá-lo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-285">There are some services that can help you with this.</span></span> <span data-ttu-id="e6fcb-286">Você pode também crie seu próprios, como servidor de tooa arquivo hello envio.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="e6fcb-287">Estes são os níveis de log hello:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-287">These are hello logging levels:</span></span>
* <span data-ttu-id="e6fcb-288">Erro (exceções)</span><span class="sxs-lookup"><span data-stu-id="e6fcb-288">Error (exceptions)</span></span>
* <span data-ttu-id="e6fcb-289">Aviso (aviso)</span><span class="sxs-lookup"><span data-stu-id="e6fcb-289">Warn (warning)</span></span>
* <span data-ttu-id="e6fcb-290">Informações (fins informativos)</span><span class="sxs-lookup"><span data-stu-id="e6fcb-290">Info (information purposes)</span></span>
* <span data-ttu-id="e6fcb-291">Detalhado (mais detalhes)</span><span class="sxs-lookup"><span data-stu-id="e6fcb-291">Verbose (more details)</span></span>

<span data-ttu-id="e6fcb-292">Você definir o nível de log de saudação assim:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="e6fcb-293">Todas as mensagens de log são enviadas toologcat, em retornos de chamada adição tooany log personalizado.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="e6fcb-294">Você pode obter um arquivo de log tooa de logcat da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="e6fcb-295">Para obter detalhes sobre comandos adb, consulte Olá [logcat informações no site Android Olá](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="e6fcb-296">Rastreamentos de rede</span><span class="sxs-lookup"><span data-stu-id="e6fcb-296">Network traces</span></span>
<span data-ttu-id="e6fcb-297">Você pode usar várias ferramentas toocapture Olá tráfego HTTP que gera ADAL.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="e6fcb-298">Isso é mais útil se você estiver familiarizado com hello protocolo OAuth ou se você precisar tooprovide tooMicrosoft de informações de diagnóstico ou outros canais de suporte.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="e6fcb-299">O Fiddler é uma ferramenta de rastreamento de HTTP mais fácil hello.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="e6fcb-300">A seguir use Olá links tooset-toocorrectly registro ADAL tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="e6fcb-301">Para uma ferramenta de rastreamento como o Fiddler ou Charles toobe útil, você deve configurá-lo toorecord sem criptografia SSL tráfego.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="e6fcb-302">Rastreamentos gerados desta forma podem conter informações altamente privilegiadas como tokens de acesso, nomes de usuário e senhas.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="e6fcb-303">Se você estiver usando contas de produção, não compartilhe esses rastreamentos com terceiros.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="e6fcb-304">Se você precisar toosupply toosomeone um rastreamento no suporte a ordem tooget, reproduza o problema de saudação usando uma conta temporária com nomes de usuário e senhas que você não se importar de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="e6fcb-305">Do site de Telerik Olá: [configuração o Fiddler para Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="e6fcb-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="e6fcb-306">Do GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler) (Configurar regras do Fiddler para ADAL)</span><span class="sxs-lookup"><span data-stu-id="e6fcb-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="e6fcb-307">Modo de caixa de diálogo</span><span class="sxs-lookup"><span data-stu-id="e6fcb-307">Dialog mode</span></span>
<span data-ttu-id="e6fcb-308">método de acquireToken Hello sem atividade dá suporte a um prompt da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="e6fcb-309">Criptografia</span><span class="sxs-lookup"><span data-stu-id="e6fcb-309">Encryption</span></span>
<span data-ttu-id="e6fcb-310">ADAL criptografa tokens hello e armazenamento em SharedPreferences por padrão.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="e6fcb-311">Você pode ver detalhes de Olá Olá StorageHelper classe toosee.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="e6fcb-312">O Android introduziu o Armazenamento de chaves privadas Android KeyStore 4.3 (API 18).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="e6fcb-313">A ADAL o utiliza para API18 e superior.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="e6fcb-314">Se você quiser toouse ADAL para versões anteriores do SDK, você precisa tooprovide uma chave de segredo AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="e6fcb-315">Desafio de portador do Oauth2</span><span class="sxs-lookup"><span data-stu-id="e6fcb-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="e6fcb-316">Olá AuthenticationParameters classe fornece funcionalidade tooget authorization_uri de saudação desafio de portador de OAuth2.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="e6fcb-317">Cookies de sessão no Webview</span><span class="sxs-lookup"><span data-stu-id="e6fcb-317">Session cookies in WebView</span></span>
<span data-ttu-id="e6fcb-318">WebView Android não limpar cookies de sessão depois que o aplicativo hello está fechado.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="e6fcb-319">Você pode tratar disso usando este exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="e6fcb-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="e6fcb-320">Para obter detalhes sobre os cookies, consulte Olá [CookieSyncManager informações no site Android Olá](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="e6fcb-321">Substituições de recurso</span><span class="sxs-lookup"><span data-stu-id="e6fcb-321">Resource overrides</span></span>
<span data-ttu-id="e6fcb-322">Biblioteca da ADAL Olá inclui cadeias de caracteres em inglês de ProgressDialog.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="e6fcb-323">Seu aplicativo deve substituí-las se você quiser cadeias de caracteres localizadas.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="e6fcb-324">Caixa de diálogo NTLM</span><span class="sxs-lookup"><span data-stu-id="e6fcb-324">NTLM dialog box</span></span>
<span data-ttu-id="e6fcb-325">Versão da ADAL 1.1.0 dá suporte a uma caixa de diálogo NTLM que é processada por meio do evento de onReceivedHttpAuthRequest de saudação do WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="e6fcb-326">Você pode personalizar o layout de saudação e cadeias de caracteres para a caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e6fcb-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="e6fcb-327">SSO entre aplicativos</span><span class="sxs-lookup"><span data-stu-id="e6fcb-327">Cross-app SSO</span></span>
<span data-ttu-id="e6fcb-328">Saiba [como tooenable SSO entre aplicativo no Android usando o ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="e6fcb-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
