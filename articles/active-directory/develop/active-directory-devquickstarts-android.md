---
title: "Introdução a Android no AD do Azure | Microsoft Docs"
description: Como compilar um aplicativo para Android que se integre ao Azure AD para entrada e que chame as APIs protegidas do Azure AD usando o OAuth.
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
ms.openlocfilehash: 746cad19093fd2a1ad23ddd9412394f8d9da331c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="562bb-103">Integração do Azure AD a um aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="562bb-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="562bb-104">Experimente a versão de visualização de nosso novo [portal do desenvolvedor](https://identity.microsoft.com/Docs/Android), que ajudará você a executar o Azure AD em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="562bb-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="562bb-105">O portal do desenvolvedor orientará você pelo processo de registro de um aplicativo e integração do Azure AD em seu código.</span><span class="sxs-lookup"><span data-stu-id="562bb-105">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="562bb-106">Quando terminar, você terá um aplicativo simples que pode autenticar os usuários em seu locatário e um back-end que pode aceitar tokens e executar a validação.</span><span class="sxs-lookup"><span data-stu-id="562bb-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="562bb-107">Se você estiver desenvolvendo um aplicativo da área de trabalho, o Azure AD (Azure Active Directory) simplificará a autenticação dos usuários com as próprias contas do Active Directory locais.</span><span class="sxs-lookup"><span data-stu-id="562bb-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="562bb-108">Ele também permite que seu aplicativo consuma com segurança qualquer API da Web protegida pelo AD do Azure, como as APIs do Office 365 ou a API do Azure.</span><span class="sxs-lookup"><span data-stu-id="562bb-108">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="562bb-109">Para os clientes Android que precisam acessar recursos protegidos, o Azure AD fornece a ADAL (Biblioteca de Autenticação do Active Directory).</span><span class="sxs-lookup"><span data-stu-id="562bb-109">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="562bb-110">A única finalidade da ADAL é tornar mais fácil para seu aplicativo obter tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="562bb-110">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="562bb-111">Para demonstrar como isso é fácil, vamos compilar um aplicativo de lista de tarefas pendentes para Android que:</span><span class="sxs-lookup"><span data-stu-id="562bb-111">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="562bb-112">Obtém tokens de acesso para chamar a API da lista de tarefas pendentes usando o [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="562bb-112">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="562bb-113">Obtém a lista de tarefas pendentes de um usuário.</span><span class="sxs-lookup"><span data-stu-id="562bb-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="562bb-114">Desconecta usuários.</span><span class="sxs-lookup"><span data-stu-id="562bb-114">Signs out users.</span></span>

<span data-ttu-id="562bb-115">Para começar, você precisa de um locatário do Azure AD no qual possa criar usuários e registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="562bb-115">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="562bb-116">Se você ainda não tiver um locatário [saiba como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="562bb-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="562bb-117">Etapa 1: Baixe e execute o servidor de exemplo API REST TODO do Node. js</span><span class="sxs-lookup"><span data-stu-id="562bb-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="562bb-118">O servidor de exemplo REST API TODO do Node.js é escrito especificamente para funcionar em nosso exemplo, a fim de criar uma API REST de tarefas pendentes de locatário único para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="562bb-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="562bb-119">Este é um pré-requisito para o Início Rápido.</span><span class="sxs-lookup"><span data-stu-id="562bb-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="562bb-120">Para obter informações sobre como configurar isso, consulte nossos exemplos em [Serviço de API REST de exemplo para Node. js do Microsoft Azure Active Directory](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="562bb-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="562bb-121">Etapa 2: Registre sua API da Web com seu locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="562bb-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="562bb-122">O Active Directory dá suporte à adição de dois tipos de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="562bb-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="562bb-123">APIs da Web que oferecem serviços a usuários</span><span class="sxs-lookup"><span data-stu-id="562bb-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="562bb-124">Aplicativos (executados na Web ou em um dispositivo) que acessam essas APIs da Web</span><span class="sxs-lookup"><span data-stu-id="562bb-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="562bb-125">Nesta etapa, você está registrando a API da Web que está sendo executada localmente para testar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="562bb-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="562bb-126">Normalmente, essa API da Web é um serviço REST que oferece uma funcionalidade interessante a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="562bb-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="562bb-127">O Azure AD pode ajudar a proteger qualquer ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="562bb-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="562bb-128">Vamos supor que você esteja registrando a API REST TODO mencionada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="562bb-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="562bb-129">Porém, isso funciona para qualquer API da Web para a qual você queira proteção do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="562bb-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="562bb-130">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="562bb-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="562bb-131">Na barra superior, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="562bb-131">On the top bar, click your account.</span></span> <span data-ttu-id="562bb-132">Na lista **Diretório**, escolha o locatário do Azure AD no qual você quer registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="562bb-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="562bb-133">Clique em **Mais Serviços** no painel esquerdo e selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="562bb-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="562bb-134">Clique em **Registros do aplicativo**e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="562bb-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="562bb-135">Insira um nome amigável para o aplicativo (por exemplo, **TodoListService**, selecione **Aplicativo Web e/ou API da Web** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="562bb-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="562bb-136">Para a URL de logon, insira a URL base para o exemplo.</span><span class="sxs-lookup"><span data-stu-id="562bb-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="562bb-137">Por padrão, ela é `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="562bb-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="562bb-138">Clique em **OK** para concluir o registro.</span><span class="sxs-lookup"><span data-stu-id="562bb-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="562bb-139">Ainda no Portal do Azure, acesse a página de aplicativo, encontre o valor da ID do aplicativo e copie-o.</span><span class="sxs-lookup"><span data-stu-id="562bb-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="562bb-140">Você precisará dele mais tarde ao configurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="562bb-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="562bb-141">Na página **Configurações** -> **Propriedades**, atualize o URI da ID do aplicativo – insira `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="562bb-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="562bb-142">Substitua `<your_tenant_name>` pelo nome de seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="562bb-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="562bb-143">Etapa 3: Registre o aplicativo cliente nativo para Android de exemplo</span><span class="sxs-lookup"><span data-stu-id="562bb-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="562bb-144">Registre seu aplicativo da Web neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="562bb-144">You must register your web application in this sample.</span></span> <span data-ttu-id="562bb-145">Isso permite que o aplicativo se comunique com a API da Web recém-registrada.</span><span class="sxs-lookup"><span data-stu-id="562bb-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="562bb-146">O Azure AD não vai permitir que o aplicativo solicite a entrada a menos que ele esteja registrado.</span><span class="sxs-lookup"><span data-stu-id="562bb-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="562bb-147">Isso faz parte da segurança do modelo.</span><span class="sxs-lookup"><span data-stu-id="562bb-147">That's part of the security of the model.</span></span>

<span data-ttu-id="562bb-148">Vamos supor que você esteja registrando o exemplo de aplicativo mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="562bb-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="562bb-149">Porém, este procedimento funciona para qualquer aplicativo que você esteja desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="562bb-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="562bb-150">Talvez você se pergunte por que está colocando um aplicativo e uma API da Web em um locatário.</span><span class="sxs-lookup"><span data-stu-id="562bb-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="562bb-151">Como você deve ter adivinhado, é possível compilar um aplicativo que acessa uma API externa que é registrada no Azure AD de outro locatário.</span><span class="sxs-lookup"><span data-stu-id="562bb-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="562bb-152">Se você fizer isso, os clientes precisarão concordar com o uso da API no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="562bb-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="562bb-153">A biblioteca de autenticação do Active Directory para iOS se encarrega desse consentimento por você.</span><span class="sxs-lookup"><span data-stu-id="562bb-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="562bb-154">Conforme exploramos recursos mais avançados, você verá que essa é uma parte importante do trabalho necessário para acessar o conjunto de APIs da Microsoft no Azure e Office, bem como em qualquer outro provedor de serviço.</span><span class="sxs-lookup"><span data-stu-id="562bb-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="562bb-155">Por enquanto, como você registrou sua API da Web e seu aplicativo sob o mesmo locatário, você não verá solicitações de permissão.</span><span class="sxs-lookup"><span data-stu-id="562bb-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="562bb-156">Isso normalmente acontece se você estiver desenvolvendo um aplicativo para uso exclusivo de sua própria empresa.</span><span class="sxs-lookup"><span data-stu-id="562bb-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="562bb-157">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="562bb-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="562bb-158">Na barra superior, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="562bb-158">On the top bar, click your account.</span></span> <span data-ttu-id="562bb-159">Na lista **Diretório**, escolha o locatário do Azure AD no qual você quer registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="562bb-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="562bb-160">Clique em **Mais Serviços** no painel esquerdo e selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="562bb-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="562bb-161">Clique em **Registros do aplicativo**e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="562bb-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="562bb-162">Insira um nome amigável para o aplicativo (por exemplo, **TodoListClient-Android**), selecione **Aplicativo Cliente Nativo** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="562bb-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="562bb-163">Para o URI de redirecionamento, insira `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="562bb-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="562bb-164">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="562bb-164">Click **Finish**.</span></span>
7. <span data-ttu-id="562bb-165">Na página do aplicativo, encontre o valor da ID do aplicativo e copie-o.</span><span class="sxs-lookup"><span data-stu-id="562bb-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="562bb-166">Você precisará dele mais tarde ao configurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="562bb-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="562bb-167">Na página **Configurações**, escolha **Permissões Necessárias** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="562bb-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="562bb-168">Localize e selecione TodoListService e adicione a permissão **Acessar TodoListService** em **Permissões Delegadas** e clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="562bb-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="562bb-169">Para compilar com o Maven, use o pom.xml de nível superior:</span><span class="sxs-lookup"><span data-stu-id="562bb-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="562bb-170">Clone esse repositório em um diretório de sua escolha:</span><span class="sxs-lookup"><span data-stu-id="562bb-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="562bb-171">Siga as etapas nos [pré-requisitos de configuração de seu ambiente Maven para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="562bb-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="562bb-172">Configure o emulador com o SDK 19.</span><span class="sxs-lookup"><span data-stu-id="562bb-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="562bb-173">Vá para a pasta raiz onde você clonou o repositório.</span><span class="sxs-lookup"><span data-stu-id="562bb-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="562bb-174">Execute este comando: `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="562bb-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="562bb-175">Altere o diretório para o exemplo do Início Rápido: `cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="562bb-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="562bb-176">Execute este comando: `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="562bb-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="562bb-177">O aplicativo deve iniciar.</span><span class="sxs-lookup"><span data-stu-id="562bb-177">You should see the app starting.</span></span>
8. <span data-ttu-id="562bb-178">Insira as credenciais de usuário de teste para experimentar.</span><span class="sxs-lookup"><span data-stu-id="562bb-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="562bb-179">Pacotes JAR serão enviados juntamente com o pacote AAR.</span><span class="sxs-lookup"><span data-stu-id="562bb-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="562bb-180">Etapa 4: Baixe a ADAL para Android e adicione-a ao seu espaço de trabalho do Eclipse</span><span class="sxs-lookup"><span data-stu-id="562bb-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="562bb-181">Facilitamos para você ter várias opções para usar a ADAL em seu projeto para Android:</span><span class="sxs-lookup"><span data-stu-id="562bb-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="562bb-182">Você pode usar o código-fonte para importar essa biblioteca no Eclipse e vinculá-la ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="562bb-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="562bb-183">Se estiver usando o Android Studio, você poderá usar o formato de pacote AAR e fazer referência aos binários.</span><span class="sxs-lookup"><span data-stu-id="562bb-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="562bb-184">Opção 1: zip de origem</span><span class="sxs-lookup"><span data-stu-id="562bb-184">Option 1: Source Zip</span></span>
<span data-ttu-id="562bb-185">Para baixar uma cópia do código-fonte, clique em **Baixar ZIP** no lado direito da página.</span><span class="sxs-lookup"><span data-stu-id="562bb-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="562bb-186">Ou [baixe do GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="562bb-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="562bb-187">Opção 2: Origem via Git</span><span class="sxs-lookup"><span data-stu-id="562bb-187">Option 2: Source via Git</span></span>
<span data-ttu-id="562bb-188">Para obter o código-fonte do SDK via Git, digite:</span><span class="sxs-lookup"><span data-stu-id="562bb-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="562bb-189">Opção 3: Binários via Gradle</span><span class="sxs-lookup"><span data-stu-id="562bb-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="562bb-190">Você pode obter os binários do repositório central do Maven.</span><span class="sxs-lookup"><span data-stu-id="562bb-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="562bb-191">O pacote AAR pode ser incluído da seguinte forma em seu projeto no Android Studio:</span><span class="sxs-lookup"><span data-stu-id="562bb-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

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

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="562bb-192">Opção 4: AAR via Maven</span><span class="sxs-lookup"><span data-stu-id="562bb-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="562bb-193">Se você estiver usando o plug-in M2Eclipse no Eclipse, especifique a dependência em seu arquivo pom.xml:</span><span class="sxs-lookup"><span data-stu-id="562bb-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="562bb-194">Opção 5: pacote JAR dentro da pasta de bibliotecas</span><span class="sxs-lookup"><span data-stu-id="562bb-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="562bb-195">Você pode obter o arquivo JAR do repositório Maven e colocá-lo na pasta **libs** em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="562bb-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="562bb-196">Você também precisa copiar os recursos necessários ao seu projeto, uma vez que os pacotes JAR não os incluem.</span><span class="sxs-lookup"><span data-stu-id="562bb-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="562bb-197">Etapa 5: Adicione referências à ADAL do Android em seu projeto</span><span class="sxs-lookup"><span data-stu-id="562bb-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="562bb-198">Adicione uma referência ao seu projeto e especifique-a como uma biblioteca Android.</span><span class="sxs-lookup"><span data-stu-id="562bb-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="562bb-199">Se você não tiver certeza sobre como fazer isso, saiba mais no [site do Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="562bb-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="562bb-200">Adicione a dependência do projeto para depuração nas configurações de seu projeto.</span><span class="sxs-lookup"><span data-stu-id="562bb-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="562bb-201">Atualize o arquivo AndroidManifest.xml do seu projeto para incluir:</span><span class="sxs-lookup"><span data-stu-id="562bb-201">Update your project's AndroidManifest.xml file to include:</span></span>

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

4. <span data-ttu-id="562bb-202">Crie uma instância de AuthenticationContext na atividade principal.</span><span class="sxs-lookup"><span data-stu-id="562bb-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="562bb-203">Os detalhes dessa chamada estão além do escopo deste tópico, mas você pode obter uma boa introdução com o [exemplo de cliente nativo para Android](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="562bb-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="562bb-204">No exemplo a seguir, SharedPreferences é o cache padrão, e a Autoridade está na forma de `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="562bb-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="562bb-205">Copie esse bloco de código para lidar com o final de AuthenticationActivity, após o usuário inserir as credenciais e receber o código de autorização:</span><span class="sxs-lookup"><span data-stu-id="562bb-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="562bb-206">Para solicitar um token, defina um retorno de chamada:</span><span class="sxs-lookup"><span data-stu-id="562bb-206">To ask for a token, define a callback:</span></span>

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

7. <span data-ttu-id="562bb-207">Por fim, solicite um token usando esse retorno de chamada:</span><span class="sxs-lookup"><span data-stu-id="562bb-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="562bb-208">Confira uma explicação dos parâmetros:</span><span class="sxs-lookup"><span data-stu-id="562bb-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="562bb-209">*resource* é obrigatório e é o recurso que você está tentando acessar.</span><span class="sxs-lookup"><span data-stu-id="562bb-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="562bb-210">*clientid* é obrigatório e é proveniente do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="562bb-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="562bb-211">*RedirectUri* não é obrigatório para a chamada acquireToken.</span><span class="sxs-lookup"><span data-stu-id="562bb-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="562bb-212">Configure-o como o nome de seu pacote.</span><span class="sxs-lookup"><span data-stu-id="562bb-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="562bb-213">*PromptBehavior* ajuda a solicitar credenciais para ignorar o cache e o cookie.</span><span class="sxs-lookup"><span data-stu-id="562bb-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="562bb-214">*callback* será chamado depois que o código de autorização for trocado por um token.</span><span class="sxs-lookup"><span data-stu-id="562bb-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="562bb-215">Ele possui um objeto AuthenticationResult, que tem informações sobre o token de acesso, a data de vencimento e o token de ID.</span><span class="sxs-lookup"><span data-stu-id="562bb-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="562bb-216">*acquireTokenSilent* é opcional.</span><span class="sxs-lookup"><span data-stu-id="562bb-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="562bb-217">Você pode chamá-lo para manipular o cache e a atualização do token.</span><span class="sxs-lookup"><span data-stu-id="562bb-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="562bb-218">Ele também fornece a versão de sincronização.</span><span class="sxs-lookup"><span data-stu-id="562bb-218">It also provides the sync version.</span></span> <span data-ttu-id="562bb-219">Ele aceita *userid* como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="562bb-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="562bb-220">Usando este passo a passo, você deve ter o que precisa para se integrar com êxito com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="562bb-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="562bb-221">Para obter mais exemplos de como isso funciona, visite o repositório AzureADSamples/ no GitHub.</span><span class="sxs-lookup"><span data-stu-id="562bb-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="562bb-222">Informações importantes</span><span class="sxs-lookup"><span data-stu-id="562bb-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="562bb-223">Personalização</span><span class="sxs-lookup"><span data-stu-id="562bb-223">Customization</span></span>
<span data-ttu-id="562bb-224">Os recursos de seu aplicativo podem substituir os recursos de projeto da biblioteca.</span><span class="sxs-lookup"><span data-stu-id="562bb-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="562bb-225">Isso acontece quando seu aplicativo está sendo compilado.</span><span class="sxs-lookup"><span data-stu-id="562bb-225">This happens when your app is being built.</span></span> <span data-ttu-id="562bb-226">Por esse motivo, você pode personalizar o layout de atividade de autenticação da maneira desejada.</span><span class="sxs-lookup"><span data-stu-id="562bb-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="562bb-227">Lembre-se de manter a ID dos controles usados pela ADAL (WebView).</span><span class="sxs-lookup"><span data-stu-id="562bb-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="562bb-228">Agente</span><span class="sxs-lookup"><span data-stu-id="562bb-228">Broker</span></span>
<span data-ttu-id="562bb-229">O aplicativo do portal da empresa do Microsoft Intune fornece o componente do agente.</span><span class="sxs-lookup"><span data-stu-id="562bb-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="562bb-230">A conta é criada no AccountManager.</span><span class="sxs-lookup"><span data-stu-id="562bb-230">The account is created in AccountManager.</span></span> <span data-ttu-id="562bb-231">O tipo de conta é "com.microsoft.workaccount".</span><span class="sxs-lookup"><span data-stu-id="562bb-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="562bb-232">AccountManager permite apenas uma única conta SSO.</span><span class="sxs-lookup"><span data-stu-id="562bb-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="562bb-233">Ele cria o cookie do SSO para o usuário após a conclusão do desafio do dispositivo para um dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="562bb-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="562bb-234">A ADAL usa a conta de agente se houver uma conta de usuário criada nesse autenticador, e você optar por não ignorá-la.</span><span class="sxs-lookup"><span data-stu-id="562bb-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="562bb-235">Você pode ignorar o usuário do agente com:</span><span class="sxs-lookup"><span data-stu-id="562bb-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="562bb-236">Você precisa registrar um redirectUri especial para uso do agente.</span><span class="sxs-lookup"><span data-stu-id="562bb-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="562bb-237">RedirectUri está no formato `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="562bb-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="562bb-238">Você pode obter o RedirectUri para seu aplicativo usando o script brokerRedirectPrint.ps1 ou usar a chamada à API mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="562bb-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="562bb-239">A assinatura está relacionada aos seus certificados de autenticação.</span><span class="sxs-lookup"><span data-stu-id="562bb-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="562bb-240">O modelo atual do agente é para um usuário.</span><span class="sxs-lookup"><span data-stu-id="562bb-240">The current broker model is for one user.</span></span> <span data-ttu-id="562bb-241">AuthenticationContext fornece o método de API para obter o usuário do agente.</span><span class="sxs-lookup"><span data-stu-id="562bb-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="562bb-242">O manifesto de seu aplicativo deve ter as seguintes permissões para usar contas do AccountManager.</span><span class="sxs-lookup"><span data-stu-id="562bb-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="562bb-243">Para obter detalhes, consulte as [Informações do AccountManager no site do Android](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="562bb-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="562bb-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="562bb-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="562bb-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="562bb-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="562bb-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="562bb-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="562bb-247">URL da Autoridade e AD FS</span><span class="sxs-lookup"><span data-stu-id="562bb-247">Authority URL and AD FS</span></span>
<span data-ttu-id="562bb-248">O AD FS (Serviços de Federação do Active Directory) não é reconhecido como STS de produção, por isso, você precisa desativar a descoberta de instância e inserir false no construtor de AuthenticationContext.</span><span class="sxs-lookup"><span data-stu-id="562bb-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="562bb-249">A URL da autoridade precisa de uma instância STS e de um [nome de locatário](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="562bb-249">The authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="562bb-250">Consultar itens do cache</span><span class="sxs-lookup"><span data-stu-id="562bb-250">Querying cache items</span></span>
<span data-ttu-id="562bb-251">A ADAL fornece um cache padrão em SharedPreferences com algumas funções de consulta de cache simples.</span><span class="sxs-lookup"><span data-stu-id="562bb-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="562bb-252">É possível obter o cache atual de AuthenticationContext usando:</span><span class="sxs-lookup"><span data-stu-id="562bb-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="562bb-253">Também será possível fornecer implementação ao cache, se desejar personalizá-lo.</span><span class="sxs-lookup"><span data-stu-id="562bb-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="562bb-254">Comportamento da solicitação</span><span class="sxs-lookup"><span data-stu-id="562bb-254">Prompt behavior</span></span>
<span data-ttu-id="562bb-255">A ADAL fornece uma opção para especificar o comportamento da solicitação.</span><span class="sxs-lookup"><span data-stu-id="562bb-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="562bb-256">PromptBehavior.Auto exibirá a interface do usuário se o token de atualização for inválido e as credenciais de usuário forem exigidas.</span><span class="sxs-lookup"><span data-stu-id="562bb-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="562bb-257">PromptBehavior.Always ignorará o uso de cache e sempre mostrará a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="562bb-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="562bb-258">Solicitação de token silenciosa do cache e atualização</span><span class="sxs-lookup"><span data-stu-id="562bb-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="562bb-259">Uma solicitação de token silenciosa não usa o pop-up da interface do usuário e não exige uma atividade.</span><span class="sxs-lookup"><span data-stu-id="562bb-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="562bb-260">Ele retorna um token do cache, se estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="562bb-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="562bb-261">Se o token tiver expirado, esse método tenta atualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="562bb-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="562bb-262">Se o token de atualização tiver expirado ou falhado, ele retornará AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="562bb-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="562bb-263">Você também pode fazer uma chamada de sincronização com esse método.</span><span class="sxs-lookup"><span data-stu-id="562bb-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="562bb-264">Você pode definir null para retorno de chamada ou usar acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="562bb-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="562bb-265">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="562bb-265">Diagnostics</span></span>
<span data-ttu-id="562bb-266">Estas são as principais fontes de informações para diagnosticar problemas:</span><span class="sxs-lookup"><span data-stu-id="562bb-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="562bb-267">Exceções</span><span class="sxs-lookup"><span data-stu-id="562bb-267">Exceptions</span></span>
* <span data-ttu-id="562bb-268">Logs</span><span class="sxs-lookup"><span data-stu-id="562bb-268">Logs</span></span>
* <span data-ttu-id="562bb-269">Rastreamentos de rede</span><span class="sxs-lookup"><span data-stu-id="562bb-269">Network traces</span></span>

<span data-ttu-id="562bb-270">Observe que as IDs de correlação são essenciais para o diagnóstico na biblioteca.</span><span class="sxs-lookup"><span data-stu-id="562bb-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="562bb-271">Você pode definir suas IDs de correlação com base em cada solicitação se quiser correlacionar uma solicitação da ADAL com outras operações em seu código.</span><span class="sxs-lookup"><span data-stu-id="562bb-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="562bb-272">Se você não definir uma ID de correlação, a ADAL gerará uma senha aleatória.</span><span class="sxs-lookup"><span data-stu-id="562bb-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="562bb-273">Todas as mensagens de log e chamadas de rede serão carimbadas com a ID de correlação.</span><span class="sxs-lookup"><span data-stu-id="562bb-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="562bb-274">A ID gerada automaticamente muda em cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="562bb-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="562bb-275">Exceções</span><span class="sxs-lookup"><span data-stu-id="562bb-275">Exceptions</span></span>
<span data-ttu-id="562bb-276">As exceções são o primeiro diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="562bb-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="562bb-277">Tentamos fornecer mensagens de erro úteis.</span><span class="sxs-lookup"><span data-stu-id="562bb-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="562bb-278">Se você encontrar uma que não é útil, registre um problema e nos informe.</span><span class="sxs-lookup"><span data-stu-id="562bb-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="562bb-279">Inclua informações do dispositivo, como modelo e número do SDK.</span><span class="sxs-lookup"><span data-stu-id="562bb-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="562bb-280">Logs</span><span class="sxs-lookup"><span data-stu-id="562bb-280">Logs</span></span>
<span data-ttu-id="562bb-281">Você pode configurar a biblioteca para gerar mensagens de log que você pode usar para ajudar a diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="562bb-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="562bb-282">Configure o registro de log fazendo a chamada a seguir para configurar um retorno de chamada que a ADAL usará para lidar com cada mensagem de log conforme elas são geradas.</span><span class="sxs-lookup"><span data-stu-id="562bb-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="562bb-283">As mensagens podem ser gravadas em um arquivo de log personalizado, conforme visto no código a seguir.</span><span class="sxs-lookup"><span data-stu-id="562bb-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="562bb-284">Infelizmente, não há um modo padrão de obter os logs de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="562bb-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="562bb-285">Há alguns serviços que podem ajudá-lo.</span><span class="sxs-lookup"><span data-stu-id="562bb-285">There are some services that can help you with this.</span></span> <span data-ttu-id="562bb-286">Você pode também criar seus próprios métodos, como enviar o arquivo para um servidor.</span><span class="sxs-lookup"><span data-stu-id="562bb-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="562bb-287">Estes são os níveis de log:</span><span class="sxs-lookup"><span data-stu-id="562bb-287">These are the logging levels:</span></span>
* <span data-ttu-id="562bb-288">Erro (exceções)</span><span class="sxs-lookup"><span data-stu-id="562bb-288">Error (exceptions)</span></span>
* <span data-ttu-id="562bb-289">Aviso (aviso)</span><span class="sxs-lookup"><span data-stu-id="562bb-289">Warn (warning)</span></span>
* <span data-ttu-id="562bb-290">Informações (fins informativos)</span><span class="sxs-lookup"><span data-stu-id="562bb-290">Info (information purposes)</span></span>
* <span data-ttu-id="562bb-291">Detalhado (mais detalhes)</span><span class="sxs-lookup"><span data-stu-id="562bb-291">Verbose (more details)</span></span>

<span data-ttu-id="562bb-292">Defina o nível de log da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="562bb-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="562bb-293">Todas as mensagens de log são enviadas para logcat, além de qualquer retorno de chamada de log personalizado.</span><span class="sxs-lookup"><span data-stu-id="562bb-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="562bb-294">Você pode obter um log para um arquivo do logcat da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="562bb-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="562bb-295">Para obter detalhes sobre comandos adb, consulte as [informações sobre o logcat no site da Android](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="562bb-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="562bb-296">Rastreamentos de rede</span><span class="sxs-lookup"><span data-stu-id="562bb-296">Network traces</span></span>
<span data-ttu-id="562bb-297">Você pode usar várias ferramentas para capturar o tráfego HTTP que a ADAL gera.</span><span class="sxs-lookup"><span data-stu-id="562bb-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="562bb-298">Isso é mais útil se você estiver familiarizado com o protocolo OAuth ou se você precisar fornecer informações de diagnóstico para a Microsoft ou outros canais de suporte.</span><span class="sxs-lookup"><span data-stu-id="562bb-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="562bb-299">Fiddler é a ferramenta de rastreamento de HTTP mais fácil.</span><span class="sxs-lookup"><span data-stu-id="562bb-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="562bb-300">Use os links a seguir para configurá-la até o tráfego de rede da ADAL de registro correto.</span><span class="sxs-lookup"><span data-stu-id="562bb-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="562bb-301">Para que uma ferramenta de rastreamento, como o Fiddler ou Charles, seja útil, você deve configurá-la para registrar o tráfego SSL não criptografado.</span><span class="sxs-lookup"><span data-stu-id="562bb-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="562bb-302">Rastreamentos gerados desta forma podem conter informações altamente privilegiadas como tokens de acesso, nomes de usuário e senhas.</span><span class="sxs-lookup"><span data-stu-id="562bb-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="562bb-303">Se você estiver usando contas de produção, não compartilhe esses rastreamentos com terceiros.</span><span class="sxs-lookup"><span data-stu-id="562bb-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="562bb-304">Se precisar fornecer um rastreamento a alguém para obter suporte, reproduza o problema com uma conta temporária com nomes de usuário e senhas que você não se importa de compartilhar.</span><span class="sxs-lookup"><span data-stu-id="562bb-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="562bb-305">Do site da Telerik: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid) (Configuração o Fiddler para Android)</span><span class="sxs-lookup"><span data-stu-id="562bb-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="562bb-306">Do GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler) (Configurar regras do Fiddler para ADAL)</span><span class="sxs-lookup"><span data-stu-id="562bb-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="562bb-307">Modo de caixa de diálogo</span><span class="sxs-lookup"><span data-stu-id="562bb-307">Dialog mode</span></span>
<span data-ttu-id="562bb-308">O método acquireToken sem atividade dá suporte a um prompt da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="562bb-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="562bb-309">Criptografia</span><span class="sxs-lookup"><span data-stu-id="562bb-309">Encryption</span></span>
<span data-ttu-id="562bb-310">A ADAL criptografa os tokens e os armazena em SharedPreferences por padrão.</span><span class="sxs-lookup"><span data-stu-id="562bb-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="562bb-311">Você pode examinar a classe StorageHelper para ver os detalhes.</span><span class="sxs-lookup"><span data-stu-id="562bb-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="562bb-312">O Android introduziu o Armazenamento de chaves privadas Android KeyStore 4.3 (API 18).</span><span class="sxs-lookup"><span data-stu-id="562bb-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="562bb-313">A ADAL o utiliza para API18 e superior.</span><span class="sxs-lookup"><span data-stu-id="562bb-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="562bb-314">Se você quiser usar a ADAL para versões anteriores do SDK, você precisa fornecer uma chave secreta em AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="562bb-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="562bb-315">Desafio de portador do Oauth2</span><span class="sxs-lookup"><span data-stu-id="562bb-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="562bb-316">A classe AuthenticationParameters fornece funcionalidade para obter o authorization_uri do desafio de portador do OAuth2.</span><span class="sxs-lookup"><span data-stu-id="562bb-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="562bb-317">Cookies de sessão no Webview</span><span class="sxs-lookup"><span data-stu-id="562bb-317">Session cookies in WebView</span></span>
<span data-ttu-id="562bb-318">O Android WebView não limpa os cookies de sessão depois que o aplicativo é fechado.</span><span class="sxs-lookup"><span data-stu-id="562bb-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="562bb-319">Você pode tratar disso usando este exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="562bb-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="562bb-320">Para obter detalhes sobre cookies, consulte as [informações sobre CookieSyncManager no site do Android](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="562bb-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="562bb-321">Substituições de recurso</span><span class="sxs-lookup"><span data-stu-id="562bb-321">Resource overrides</span></span>
<span data-ttu-id="562bb-322">A biblioteca ADAL inclui sequências de caracteres em inglês para mensagens ProgressDialog.</span><span class="sxs-lookup"><span data-stu-id="562bb-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="562bb-323">Seu aplicativo deve substituí-las se você quiser cadeias de caracteres localizadas.</span><span class="sxs-lookup"><span data-stu-id="562bb-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="562bb-324">Caixa de diálogo NTLM</span><span class="sxs-lookup"><span data-stu-id="562bb-324">NTLM dialog box</span></span>
<span data-ttu-id="562bb-325">A ADAL versão 1.1.0 dá suporte à caixa de diálogo NTLM, que é processada por meio do evento onReceivedHttpAuthRequest do WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="562bb-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="562bb-326">Você pode personalizar o layout e as cadeias de caracteres da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="562bb-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="562bb-327">SSO entre aplicativos</span><span class="sxs-lookup"><span data-stu-id="562bb-327">Cross-app SSO</span></span>
<span data-ttu-id="562bb-328">Saiba [como habilitar o SSO entre aplicativos no Android usando a ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="562bb-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
