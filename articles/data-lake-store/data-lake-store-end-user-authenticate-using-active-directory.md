---
title: "Autenticação do usuário final: Data Lake Store com o Azure Active Directory | Microsoft Docs"
description: "Saiba como obter a autenticação do usuário final com o Data Lake Store usando o Azure Active Directory"
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
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="b0961-103">Autenticação do usuário final com o Data Lake Store usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0961-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0961-104">Autenticação serviço a serviço</span><span class="sxs-lookup"><span data-stu-id="b0961-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="b0961-105">Autenticação do usuário final</span><span class="sxs-lookup"><span data-stu-id="b0961-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="b0961-106">O Azure Data Lake Store usa o Azure Active Directory para autenticação.</span><span class="sxs-lookup"><span data-stu-id="b0961-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="b0961-107">Antes de criar um aplicativo que funciona com o Azure Data Lake Store ou com o Azure Data Lake Analytics, primeiro você deve decidir como deseja autenticar seu aplicativo no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0961-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b0961-108">As duas principais opções disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="b0961-108">The two main options available are:</span></span>

* <span data-ttu-id="b0961-109">Autenticação do usuário final (este artigo)</span><span class="sxs-lookup"><span data-stu-id="b0961-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="b0961-110">Autenticação serviço a serviço</span><span class="sxs-lookup"><span data-stu-id="b0961-110">Service-to-service authentication</span></span>

<span data-ttu-id="b0961-111">As duas opções resultam no fornecimento de um token OAuth 2.0 a seu aplicativo, que é anexado a cada solicitação feita ao Azure Data Lake Store ou ao Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="b0961-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="b0961-112">Este artigo descreve como criar um **aplicativo nativo do Azure AD para autenticação do usuário final**.</span><span class="sxs-lookup"><span data-stu-id="b0961-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="b0961-113">Para obter instruções sobre a configuração de aplicativo do Azure AD para autenticação serviço a serviço, consulte [Autenticação serviço a serviço com o Data Lake Store usando o Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b0961-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0961-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b0961-114">Prerequisites</span></span>
* <span data-ttu-id="b0961-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0961-115">An Azure subscription.</span></span> <span data-ttu-id="b0961-116">Consulte [Obter a avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0961-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="b0961-117">A ID de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b0961-117">Your subscription ID.</span></span> <span data-ttu-id="b0961-118">Você pode habilitá-la no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0961-118">You can retrieve it from the Azure Portal.</span></span> <span data-ttu-id="b0961-119">Por exemplo, está disponível na folha da conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="b0961-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![Obter ID da assinatura](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="b0961-121">O nome de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0961-121">Your Azure AD domain name.</span></span> <span data-ttu-id="b0961-122">Você pode recuperá-lo passando o mouse sobre o canto superior direito do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0961-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span></span> <span data-ttu-id="b0961-123">Na captura de tela abaixo, o nome de domínio é **contoso.onmicrosoft.com** e o GUID entre colchetes é a ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="b0961-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![Obter domínio do AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="b0961-125">Autenticação do usuário final</span><span class="sxs-lookup"><span data-stu-id="b0961-125">End-user authentication</span></span>
<span data-ttu-id="b0961-126">Essa é a abordagem recomendada se você quer que um usuário final entre em seu aplicativo por meio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0961-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span></span> <span data-ttu-id="b0961-127">Seu aplicativo será capaz de acessar recursos do Azure com o mesmo nível de acesso do usuário final que fez logon.</span><span class="sxs-lookup"><span data-stu-id="b0961-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span></span> <span data-ttu-id="b0961-128">O usuário final precisará fornecer suas credenciais periodicamente para manter o acesso de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b0961-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="b0961-129">O resultado de fazer o usuário final entrar é que seu aplicativo recebe um token de acesso e um token de atualização.</span><span class="sxs-lookup"><span data-stu-id="b0961-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="b0961-130">O token de acesso é anexado a cada solicitação feita ao Data Lake Store ou ao Data Lake Analytics e é válido por uma hora por padrão.</span><span class="sxs-lookup"><span data-stu-id="b0961-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="b0961-131">O token de atualização pode ser usado para obter um novo token de acesso e é válido por até duas semanas, por padrão, se usado regularmente.</span><span class="sxs-lookup"><span data-stu-id="b0961-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="b0961-132">Você pode usar duas abordagens diferentes para o logon do usuário final.</span><span class="sxs-lookup"><span data-stu-id="b0961-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="b0961-133">Usando o pop-up OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="b0961-133">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="b0961-134">Seu aplicativo pode disparar um pop-up de autorização OAuth 2.0 no qual o usuário final pode inserir suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="b0961-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span></span> <span data-ttu-id="b0961-135">Essa janela pop-up também funciona com o processo de autenticação do Azure AD de dois fatores (2FA), se necessário.</span><span class="sxs-lookup"><span data-stu-id="b0961-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="b0961-136">Esse método ainda não tem suporte na ADAL (biblioteca de autenticação do Azure AD) para Python ou Java.</span><span class="sxs-lookup"><span data-stu-id="b0961-136">This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="b0961-137">Transmitindo credenciais do usuário diretamente</span><span class="sxs-lookup"><span data-stu-id="b0961-137">Directly passing in user credentials</span></span>
<span data-ttu-id="b0961-138">Seu aplicativo pode fornecer credenciais de usuário ao Azure AD diretamente.</span><span class="sxs-lookup"><span data-stu-id="b0961-138">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="b0961-139">Esse método só funciona com contas de usuário de IDs organizacionais. Ele não é compatível com contas de usuário "live ID"/pessoais, incluindo as terminadas em @outlook.com ou @live.com.</span><span class="sxs-lookup"><span data-stu-id="b0961-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="b0961-140">Além disso, esse método não é compatível com contas de usuário que requerem autenticação do Azure AD de dois fatores (2FA).</span><span class="sxs-lookup"><span data-stu-id="b0961-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-to-use-this-approach"></a><span data-ttu-id="b0961-141">O que é necessário para usar essa abordagem?</span><span class="sxs-lookup"><span data-stu-id="b0961-141">What do I need to use this approach?</span></span>
* <span data-ttu-id="b0961-142">Nome de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0961-142">Azure AD domain name.</span></span> <span data-ttu-id="b0961-143">Já está listado no pré-requisito deste artigo.</span><span class="sxs-lookup"><span data-stu-id="b0961-143">This is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="b0961-144">**Aplicativo nativo** do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0961-144">Azure AD **native application**</span></span>
* <span data-ttu-id="b0961-145">ID do aplicativo para o aplicativo nativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0961-145">Application ID for the Azure AD native application</span></span>
* <span data-ttu-id="b0961-146">URI de Redirecionamento do aplicativo nativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0961-146">Redirect URI for the Azure AD native application</span></span>
* <span data-ttu-id="b0961-147">Definir permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="b0961-147">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="b0961-148">Etapa 1: Criar um aplicativo nativo do Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0961-148">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="b0961-149">Crie e configure um aplicativo nativo do Azure AD para autenticação do usuário final com o Azure Data Lake Store usando o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0961-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="b0961-150">Para obter instruções, consulte [Criar um aplicativo do Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b0961-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="b0961-151">Ao seguir as instruções do link acima, verifique se você selecionou **Nativo** para tipo de aplicativo, conforme mostrado na captura de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="b0961-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="b0961-152">![Criar aplicativo Web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Criar aplicativo nativo")</span><span class="sxs-lookup"><span data-stu-id="b0961-152">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="b0961-153">Etapa 2: Obter a ID do aplicativo e URI de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="b0961-153">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="b0961-154">Consulte [Obter ID do aplicativo](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) para recuperar a ID do aplicativo (também chamada a ID do cliente no portal clássico do Azure) do aplicativo nativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0961-154">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application id (also called the client ID in the Azure classic portal) of the Azure AD native application.</span></span>

<span data-ttu-id="b0961-155">Para recuperar o URI de redirecionamento, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="b0961-155">To retrieve the redirect URI, follow the steps below.</span></span>

1. <span data-ttu-id="b0961-156">No Portal do Azure, selecione **Azure Active Directory**, clique em **Registros do aplicativo** e, em seguida, encontre e clique no aplicativo nativo do Azure AD que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="b0961-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="b0961-157">Na folha **Configurações** do aplicativo, clique em **URIs de Redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="b0961-157">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![Obter URI de redirecionamento](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="b0961-159">Copie o valor exibido.</span><span class="sxs-lookup"><span data-stu-id="b0961-159">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="b0961-160">Etapa 3: Definir permissões</span><span class="sxs-lookup"><span data-stu-id="b0961-160">Step 3: Set permissions</span></span>

1. <span data-ttu-id="b0961-161">No Portal do Azure, selecione **Azure Active Directory**, clique em **Registros do aplicativo** e, em seguida, encontre e clique no aplicativo nativo do Azure AD que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="b0961-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="b0961-162">Na folha **Configurações** do aplicativo, clique em **Permissões necessárias** e, em seguida, em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b0961-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![ID do CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="b0961-164">Na folha **Adicionar Acesso à API**, clique em **Selecionar uma API**, em **Azure Data Lake** e, em seguida, em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="b0961-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![ID do CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="b0961-166">Na folha **Adicionar Acesso à API**, clique em **Selecionar permissões**, marque a caixa de seleção para conceder **Acesso completo ao Data Lake Store** e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="b0961-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![ID do CLIENTE](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="b0961-168">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="b0961-168">Click **Done**.</span></span>

5. <span data-ttu-id="b0961-169">Repita as duas últimas etapas para conceder permissões à **API de Gerenciamento de Serviços do Microsoft Azure** também.</span><span class="sxs-lookup"><span data-stu-id="b0961-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="b0961-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b0961-170">Next steps</span></span>
<span data-ttu-id="b0961-171">Neste artigo, você criou um aplicativo nativo do Azure AD e reuniu as informações necessárias em seus aplicativos de cliente que você cria utilizando .NET SDK, SDK do Java, REST API etc. Agora você pode prosseguir para os artigos seguintes, que falam sobre como usar o aplicativo Web do Azure AD para primeiro se autenticar no Data Lake Store e, em seguida, executar outras operações no repositório.</span><span class="sxs-lookup"><span data-stu-id="b0961-171">In this article you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="b0961-172">Introdução ao Repositório Azure Data Lake usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b0961-172">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="b0961-173">Introdução ao Azure Data Lake Store usando o SDK do Java</span><span class="sxs-lookup"><span data-stu-id="b0961-173">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="b0961-174">Introdução ao Azure Data Lake Store usando o REST API</span><span class="sxs-lookup"><span data-stu-id="b0961-174">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

