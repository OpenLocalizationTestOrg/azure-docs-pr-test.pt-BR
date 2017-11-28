---
title: "Autenticação do usuário final: Data Lake Store com o Azure Active Directory | Microsoft Docs"
description: "Saiba como autenticação de usuário final tooachieve com repositório Data Lake usando o Active Directory do Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="f4a18-103">Autenticação do usuário final com o Data Lake Store usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4a18-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4a18-104">Autenticação serviço a serviço</span><span class="sxs-lookup"><span data-stu-id="f4a18-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="f4a18-105">Autenticação do usuário final</span><span class="sxs-lookup"><span data-stu-id="f4a18-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="f4a18-106">O Azure Data Lake Store usa o Azure Active Directory para autenticação.</span><span class="sxs-lookup"><span data-stu-id="f4a18-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="f4a18-107">Antes de criar um aplicativo que funciona com repositório Azure Data Lake ou análise Azure Data Lake, primeiro você deve decidir como você gostaria que tooauthenticate seu aplicativo com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f4a18-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f4a18-108">Olá duas opções principais disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="f4a18-108">hello two main options available are:</span></span>

* <span data-ttu-id="f4a18-109">Autenticação do usuário final (este artigo)</span><span class="sxs-lookup"><span data-stu-id="f4a18-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="f4a18-110">Autenticação serviço a serviço</span><span class="sxs-lookup"><span data-stu-id="f4a18-110">Service-to-service authentication</span></span>

<span data-ttu-id="f4a18-111">Ambas as opções resultam em seu aplicativo que está sendo fornecido com um token de OAuth 2.0, que obtém tooeach anexado solicitação feita tooAzure repositório Data Lake ou análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f4a18-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="f4a18-112">Este artigo descreve como criar um **aplicativo nativo do Azure AD para autenticação do usuário final**.</span><span class="sxs-lookup"><span data-stu-id="f4a18-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="f4a18-113">Para obter instruções sobre a configuração de aplicativo do Azure AD para autenticação serviço a serviço, consulte [Autenticação serviço a serviço com o Data Lake Store usando o Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="f4a18-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4a18-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f4a18-114">Prerequisites</span></span>
* <span data-ttu-id="f4a18-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a18-115">An Azure subscription.</span></span> <span data-ttu-id="f4a18-116">Consulte [Obter a avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4a18-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="f4a18-117">A ID de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f4a18-117">Your subscription ID.</span></span> <span data-ttu-id="f4a18-118">Você pode recuperá-lo da saudação Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a18-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="f4a18-119">Por exemplo, está disponível na folha de conta do repositório Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="f4a18-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![Obter ID da assinatura](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="f4a18-121">O nome de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4a18-121">Your Azure AD domain name.</span></span> <span data-ttu-id="f4a18-122">Você pode recuperá-la por focalização mouse Olá no canto superior direito Olá Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a18-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="f4a18-123">De saudação captura de tela abaixo, o nome de domínio de saudação é **contoso.onmicrosoft.com**, e Olá GUID entre colchetes é a ID de locatário hello.</span><span class="sxs-lookup"><span data-stu-id="f4a18-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![Obter domínio do AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="f4a18-125">Autenticação do usuário final</span><span class="sxs-lookup"><span data-stu-id="f4a18-125">End-user authentication</span></span>
<span data-ttu-id="f4a18-126">Isso é hello abordagem recomendada se você quiser um toolog do usuário final no aplicativo tooyour por meio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a18-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="f4a18-127">Seu aplicativo será capaz de tooaccess recursos do Azure com hello mesmo nível de acesso do usuário final Olá que fez logon.</span><span class="sxs-lookup"><span data-stu-id="f4a18-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="f4a18-128">O usuário final precisará tooprovide suas credenciais periodicamente para seu aplicativo toomaintain o acesso.</span><span class="sxs-lookup"><span data-stu-id="f4a18-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="f4a18-129">resultantes de saudação do login do usuário final de saudação é que o aplicativo recebe um token de acesso e um token de atualização.</span><span class="sxs-lookup"><span data-stu-id="f4a18-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="f4a18-130">token de acesso de saudação obtém tooeach anexado solicitação feita tooData Lake repositório ou análise Data Lake e é válido para uma hora, por padrão.</span><span class="sxs-lookup"><span data-stu-id="f4a18-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="f4a18-131">o token de atualização Olá pode ser usado tooobtain um novo token de acesso e é válido para o semanas tootwo por padrão, se usado regularmente.</span><span class="sxs-lookup"><span data-stu-id="f4a18-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="f4a18-132">Você pode usar duas abordagens diferentes para o logon do usuário final.</span><span class="sxs-lookup"><span data-stu-id="f4a18-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="f4a18-133">Usando a janela pop-up de saudação OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="f4a18-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="f4a18-134">Seu aplicativo pode disparar um OAuth 2.0 autorização pop-up, no qual Olá pelos usuários finais podem digitar suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="f4a18-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="f4a18-135">Essa janela pop-up também funciona com o processo de autenticação do Azure AD de dois fatores (2FA) hello, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f4a18-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4a18-136">Este método ainda não é suportado em saudação do Azure AD Authentication Library (ADAL) para Python ou Java.</span><span class="sxs-lookup"><span data-stu-id="f4a18-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="f4a18-137">Transmitindo credenciais do usuário diretamente</span><span class="sxs-lookup"><span data-stu-id="f4a18-137">Directly passing in user credentials</span></span>
<span data-ttu-id="f4a18-138">Seu aplicativo diretamente pode fornecer credenciais de usuário tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="f4a18-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="f4a18-139">Esse método só funciona com contas de usuário de IDs organizacionais. Ele não é compatível com contas de usuário "live ID"/pessoais, incluindo as terminadas em @outlook.com ou @live.com. Além disso, esse método não é compatível com contas de usuário que requerem autenticação do Azure AD de dois fatores (2FA).</span><span class="sxs-lookup"><span data-stu-id="f4a18-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="f4a18-140">O que eu preciso toouse essa abordagem?</span><span class="sxs-lookup"><span data-stu-id="f4a18-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="f4a18-141">Nome de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4a18-141">Azure AD domain name.</span></span> <span data-ttu-id="f4a18-142">Isso já está listado no pré-requisito Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="f4a18-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="f4a18-143">**Aplicativo nativo** do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4a18-143">Azure AD **native application**</span></span>
* <span data-ttu-id="f4a18-144">ID do aplicativo para o aplicativo nativo de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a18-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="f4a18-145">URI de redirecionamento para Olá aplicativo nativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f4a18-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="f4a18-146">Definir permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="f4a18-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="f4a18-147">Etapa 1: Criar um aplicativo nativo do Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4a18-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="f4a18-148">Crie e configure um aplicativo nativo do Azure AD para autenticação do usuário final com o Azure Data Lake Store usando o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4a18-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="f4a18-149">Para obter instruções, consulte [Criar um aplicativo do Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4a18-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="f4a18-150">Ao seguir as instruções Olá Olá acima link, certifique-se de selecionar **nativo** para tipo de aplicativo, conforme mostrado na captura de tela de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="f4a18-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="f4a18-151">![Criar aplicativo Web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Criar aplicativo nativo")</span><span class="sxs-lookup"><span data-stu-id="f4a18-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="f4a18-152">Etapa 2: Obter a ID do aplicativo e URI de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="f4a18-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="f4a18-153">Consulte [obter ID do aplicativo hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve Olá id de aplicativo (também chamado de ID de saudação do cliente no portal clássico do Azure de saudação) do aplicativo nativo de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4a18-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="f4a18-154">Olá tooretrieve URI de redirecionamento, execute as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="f4a18-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="f4a18-155">Olá Portal do Azure, selecione **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, localize e clique em aplicativo nativo de saudação do AD do Azure que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="f4a18-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="f4a18-156">De saudação **configurações** folha para o aplicativo hello, clique em **URIs de redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="f4a18-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![Obter URI de redirecionamento](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="f4a18-158">Copie o valor de saudação exibida.</span><span class="sxs-lookup"><span data-stu-id="f4a18-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="f4a18-159">Etapa 3: Definir permissões</span><span class="sxs-lookup"><span data-stu-id="f4a18-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="f4a18-160">Olá Portal do Azure, selecione **Active Directory do Azure**, clique em **registros do aplicativo**e, em seguida, localize e clique em aplicativo nativo de saudação do AD do Azure que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="f4a18-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="f4a18-161">De saudação **configurações** folha para o aplicativo hello, clique em **as permissões necessárias**e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f4a18-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![ID do CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="f4a18-163">Em Olá **adicionar o acesso à API** folha, clique em **selecionar uma API**, clique em **Azure Data Lake**e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="f4a18-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![ID do CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="f4a18-165">Em Olá **adicionar o acesso à API** folha, clique em **selecionar permissões**, selecione Olá toogive da caixa de seleção **completo acessar o repositório de Lake tooData**e, em seguida, clique em **selecionar **.</span><span class="sxs-lookup"><span data-stu-id="f4a18-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![ID do CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="f4a18-167">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="f4a18-167">Click **Done**.</span></span>

5. <span data-ttu-id="f4a18-168">Olá repetir último duas etapas permissões toogrant para **API de gerenciamento de serviço do Windows Azure** também.</span><span class="sxs-lookup"><span data-stu-id="f4a18-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="f4a18-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4a18-169">Next steps</span></span>
<span data-ttu-id="f4a18-170">Neste artigo, você criou um aplicativo nativo do AD do Azure e coletadas informações Olá que necessárias em seus aplicativos cliente que você cria usando o SDK do .NET, Java SDK, API REST, etc. Você pode continuar toohello artigos que falar sobre como autenticar toouse Olá AD do Azure web aplicativo toofirst repositório Data Lake e executam outras operações no repositório de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="f4a18-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="f4a18-171">Introdução ao Repositório Azure Data Lake usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="f4a18-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="f4a18-172">Introdução ao Azure Data Lake Store usando o SDK do Java</span><span class="sxs-lookup"><span data-stu-id="f4a18-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="f4a18-173">Introdução ao Azure Data Lake Store usando o REST API</span><span class="sxs-lookup"><span data-stu-id="f4a18-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

