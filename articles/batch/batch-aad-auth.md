---
title: "soluções de serviço de lote do Azure do aaaUse Active Directory do Azure tooauthenticate | Microsoft Docs"
description: "Lote dá suporte ao AD do Azure para autenticação do serviço de lote de saudação."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="dcf79-103">Autenticar soluções do serviço do Lote no Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcf79-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="dcf79-104">O Lote do Azure dá suporte à autenticação com o [Azure AD][aad_about] (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="dcf79-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="dcf79-105">O Azure AD é o serviço de gerenciamento de identidade e diretório multilocatário com base em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dcf79-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="dcf79-106">Azure próprio usa tooauthenticate do AD do Azure, seus clientes, os administradores de serviços e usuários organizacionais.</span><span class="sxs-lookup"><span data-stu-id="dcf79-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="dcf79-107">Ao usar a autenticação do Azure AD com o Lote do Azure, você pode fazer a autenticação usando uma destas duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="dcf79-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="dcf79-108">Usando **autenticação integrada** tooauthenticate um usuário que está interagindo com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="dcf79-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="dcf79-109">Um aplicativo usando a autenticação integrada reúne as credenciais do usuário e usa essas credenciais tooauthenticate acessar tooBatch os recursos.</span><span class="sxs-lookup"><span data-stu-id="dcf79-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="dcf79-110">Usando um **entidade de serviço** tooauthenticate um aplicativo autônomo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="dcf79-111">Uma entidade de serviço define permissões para um aplicativo e política de saudação no aplicativo de saudação do pedido toorepresent ao acessar recursos em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="dcf79-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="dcf79-112">toolearn mais sobre o AD do Azure, consulte Olá [documentação do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="dcf79-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="dcf79-113">Autenticação e modo de alocação de pool</span><span class="sxs-lookup"><span data-stu-id="dcf79-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="dcf79-114">Ao criar uma conta do Lote, você poderá especificar o local ao qual os pools criados para essa conta devem ser alocados.</span><span class="sxs-lookup"><span data-stu-id="dcf79-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="dcf79-115">Você pode escolher pools tooallocate na assinatura do serviço de lote saudação padrão ou em uma assinatura do usuário.</span><span class="sxs-lookup"><span data-stu-id="dcf79-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="dcf79-116">Sua escolha afeta como autenticar o acesso tooresources nessa conta.</span><span class="sxs-lookup"><span data-stu-id="dcf79-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="dcf79-117">**Assinatura do serviço do Lote**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-117">**Batch service subscription**.</span></span> <span data-ttu-id="dcf79-118">Por padrão, os pools de lote são alocados em uma assinatura de serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="dcf79-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="dcf79-119">Se você escolher essa opção, você pode autenticar acesso tooresources nessa conta com [chave compartilhada](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) ou com o AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf79-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="dcf79-120">**Assinatura de usuário.**</span><span class="sxs-lookup"><span data-stu-id="dcf79-120">**User subscription.**</span></span> <span data-ttu-id="dcf79-121">Você pode escolher tooallocate pools de lote em uma assinatura de usuário que você especificar.</span><span class="sxs-lookup"><span data-stu-id="dcf79-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="dcf79-122">Se você escolher essa opção, deverá autenticar no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcf79-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="dcf79-123">Pontos de extremidade para autenticação</span><span class="sxs-lookup"><span data-stu-id="dcf79-123">Endpoints for authentication</span></span>

<span data-ttu-id="dcf79-124">aplicativos de lote tooauthenticate com o AD do Azure, você precisa tooinclude alguns pontos de extremidade conhecidos no seu código.</span><span class="sxs-lookup"><span data-stu-id="dcf79-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="dcf79-125">Ponto de extremidade do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcf79-125">Azure AD endpoint</span></span>

<span data-ttu-id="dcf79-126">Olá base é o ponto de extremidade do AD do Azure autoridade:</span><span class="sxs-lookup"><span data-stu-id="dcf79-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="dcf79-127">tooauthenticate com o AD do Azure, você usar esse ponto de extremidade junto com a ID de locatário hello (ID de diretório).</span><span class="sxs-lookup"><span data-stu-id="dcf79-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="dcf79-128">ID de locatário Olá identifica Olá toouse de locatário do AD do Azure para autenticação.</span><span class="sxs-lookup"><span data-stu-id="dcf79-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="dcf79-129">tooretrieve Olá ID de locatário, siga etapas Olá descritas em [obter ID de locatário Olá para Active Directory do Azure](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="dcf79-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="dcf79-130">o ponto de extremidade do Hello específico de locatário é necessário quando você autenticar usando uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="dcf79-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="dcf79-131">ponto de extremidade de locatário específico de saudação é opcional quando você autenticar usando a autenticação integrada, mas recomendada.</span><span class="sxs-lookup"><span data-stu-id="dcf79-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="dcf79-132">No entanto, você também pode usar o ponto de extremidade comum Olá AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf79-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="dcf79-133">ponto de extremidade comum Olá fornece uma credencial genérica coleta interface quando um locatário específico não é fornecido.</span><span class="sxs-lookup"><span data-stu-id="dcf79-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="dcf79-134">ponto de extremidade comum Olá é `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="dcf79-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="dcf79-135">Para obter mais informações sobre pontos de extremidade do Azure AD, consulte [Cenários de autenticação do Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="dcf79-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="dcf79-136">Ponto de extremidade de recursos do Lote</span><span class="sxs-lookup"><span data-stu-id="dcf79-136">Batch resource endpoint</span></span>

<span data-ttu-id="dcf79-137">Saudação de uso **ponto de extremidade de recursos do Azure Batch** tooacquire um token para autenticar solicitações de serviço de lote toohello:</span><span class="sxs-lookup"><span data-stu-id="dcf79-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="dcf79-138">Registrar seu aplicativo em um locatário</span><span class="sxs-lookup"><span data-stu-id="dcf79-138">Register your application with a tenant</span></span>

<span data-ttu-id="dcf79-139">a primeira etapa Hello usando tooauthenticate do AD do Azure está registrando seu aplicativo em um locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf79-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="dcf79-140">Registrar seu aplicativo permite que você toocall hello Azure [biblioteca de autenticação do Active Directory] [ aad_adal] (ADAL) no seu código.</span><span class="sxs-lookup"><span data-stu-id="dcf79-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="dcf79-141">Olá ADAL fornece uma API para autenticar com o AD do Azure do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="dcf79-142">Registrar seu aplicativo é necessária se você planejar a autenticação integrada toouse ou uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="dcf79-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="dcf79-143">Quando você registra seu aplicativo, você fornece informações sobre seu aplicativo tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="dcf79-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="dcf79-144">Em seguida, o AD do Azure fornece uma ID de aplicativo que você use tooassociate seu aplicativo com o AD do Azure em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="dcf79-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="dcf79-145">toolearn mais informações sobre a ID do aplicativo hello, consulte [objetos de aplicativo e serviço principal no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="dcf79-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="dcf79-146">tooregister seu aplicativo de lote, siga etapas Olá Olá [adicionar um aplicativo](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) seção [integrando aplicativos com o Active Directory do Azure][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="dcf79-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="dcf79-147">Se você registrar seu aplicativo como um aplicativo nativo, você pode especificar qualquer URI válido para Olá **URI de redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="dcf79-148">Ele não precisa toobe um ponto de extremidade real.</span><span class="sxs-lookup"><span data-stu-id="dcf79-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="dcf79-149">Depois que você já registrou seu aplicativo, você verá a ID do aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="dcf79-149">After you've registered your application, you'll see hello application ID:</span></span>

![Registrar seu aplicativo Lote no Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="dcf79-151">Para obter mais informações sobre como registrar um aplicativo no Azure AD, consulte [Cenários de autenticação do Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="dcf79-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="dcf79-152">Obter ID de locatário de saudação do seu Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcf79-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="dcf79-153">ID de locatário Olá identifica Olá locatário do AD Azure que fornece serviços de autenticação tooyour de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="dcf79-154">tooget Olá ID de locatário, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="dcf79-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="dcf79-155">No portal do Azure de Olá, selecione seu Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dcf79-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="dcf79-156">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-156">Click **Properties**.</span></span>
3. <span data-ttu-id="dcf79-157">Copiar o valor GUID Olá fornecido para a ID de diretório hello.</span><span class="sxs-lookup"><span data-stu-id="dcf79-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="dcf79-158">Esse valor também é chamado de ID de locatário hello.</span><span class="sxs-lookup"><span data-stu-id="dcf79-158">This value is also called hello tenant ID.</span></span>

![Copiar a ID de diretório Olá](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="dcf79-160">Usar a autenticação integrada</span><span class="sxs-lookup"><span data-stu-id="dcf79-160">Use integrated authentication</span></span>

<span data-ttu-id="dcf79-161">tooauthenticate com a autenticação integrada, é necessário toogrant toohello de tooconnect de permissões seu aplicativo API do serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="dcf79-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="dcf79-162">Esta etapa permite que a sua API de serviço do aplicativo tooauthenticate chamadas toohello em lotes com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcf79-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="dcf79-163">Depois que você [registrou seu aplicativo](#register-your-application-with-an-azure-ad-tenant), siga estas etapas no hello toogrant portal do Azure que acessar o serviço de lote toohello:</span><span class="sxs-lookup"><span data-stu-id="dcf79-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="dcf79-164">No painel de navegação do lado esquerdo de saudação do Olá portal do Azure, escolha **mais serviços**, clique em **registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="dcf79-165">Pesquisar por nome de saudação do seu aplicativo na lista de saudação de registros do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="dcf79-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Procure o nome do aplicativo](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="dcf79-167">Olá abrir **configurações** folha para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="dcf79-168">Em Olá **acesso à API** seção, selecione **as permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="dcf79-169">Em Olá **as permissões necessárias** folha, clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="dcf79-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="dcf79-170">Na etapa 1, procure Olá API de lote.</span><span class="sxs-lookup"><span data-stu-id="dcf79-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="dcf79-171">Pesquisar para cada uma dessas cadeias de caracteres até encontrar hello API:</span><span class="sxs-lookup"><span data-stu-id="dcf79-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="dcf79-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="dcf79-173">**Lote do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="dcf79-174">Os locatários mais recentes do Azure AD podem usar esse nome.</span><span class="sxs-lookup"><span data-stu-id="dcf79-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="dcf79-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** é identificação Olá Olá API de lote.</span><span class="sxs-lookup"><span data-stu-id="dcf79-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="dcf79-176">Depois de encontrar hello API de lote, selecione-o e clique Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="dcf79-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="dcf79-177">Na etapa 2, selecione Olá caixa de seleção próxima muito**serviço de lote do Azure acesso** e clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="dcf79-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="dcf79-178">Clique em Olá **feito** botão.</span><span class="sxs-lookup"><span data-stu-id="dcf79-178">Click hello **Done** button.</span></span>

<span data-ttu-id="dcf79-179">Olá **permissões necessárias** folha agora mostra que o aplicativo do AD do Azure tem acesso tooboth ADAL e Olá API do serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="dcf79-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="dcf79-180">As permissões são concedidas tooADAL automaticamente quando você primeiro registra seu aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcf79-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![Conceder permissões de API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="dcf79-182">Usar uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="dcf79-182">Use a service principal</span></span> 

<span data-ttu-id="dcf79-183">tooauthenticate um aplicativo executado autônomo, você usa uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="dcf79-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="dcf79-184">Depois que você já registrou seu aplicativo, siga estas etapas no hello tooconfigure portal do Azure uma entidade de serviço:</span><span class="sxs-lookup"><span data-stu-id="dcf79-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="dcf79-185">Solicitar uma chave secreta para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="dcf79-186">Atribua um aplicativo de tooyour função RBAC.</span><span class="sxs-lookup"><span data-stu-id="dcf79-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="dcf79-187">Solicitar uma chave secreta para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="dcf79-187">Request a secret key for your application</span></span>

<span data-ttu-id="dcf79-188">Quando seu aplicativo é autenticado com uma entidade de serviço, ele envia Olá ID do aplicativo e um tooAzure chave secreta AD.</span><span class="sxs-lookup"><span data-stu-id="dcf79-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="dcf79-189">Você precisa toocreate e copiar toouse chave secreta de saudação do seu código.</span><span class="sxs-lookup"><span data-stu-id="dcf79-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="dcf79-190">Siga estas etapas no hello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="dcf79-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="dcf79-191">No painel de navegação do lado esquerdo de saudação do Olá portal do Azure, escolha **mais serviços**, clique em **registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="dcf79-192">Pesquisar por nome de saudação do seu aplicativo na lista de saudação de registros do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="dcf79-193">Saudação de exibição **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="dcf79-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="dcf79-194">Em Olá **acesso à API** seção, selecione **chaves**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="dcf79-195">toocreate uma chave, insira uma descrição para a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcf79-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="dcf79-196">Em seguida, selecione uma duração para a chave de saudação de um ou dois anos.</span><span class="sxs-lookup"><span data-stu-id="dcf79-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="dcf79-197">Clique em Olá **salvar** botão toocreate e exibir chave hello.</span><span class="sxs-lookup"><span data-stu-id="dcf79-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="dcf79-198">Copiar local seguro do tooa do valor de chave de hello, pois não será capaz de tooaccess-lo novamente depois que você deixe folha hello.</span><span class="sxs-lookup"><span data-stu-id="dcf79-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![Criar uma chave secreta](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="dcf79-200">Atribuir um aplicativo de tooyour função RBAC</span><span class="sxs-lookup"><span data-stu-id="dcf79-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="dcf79-201">tooauthenticate com uma entidade de serviço, você precisa tooassign um aplicativo de tooyour função RBAC.</span><span class="sxs-lookup"><span data-stu-id="dcf79-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="dcf79-202">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="dcf79-202">Follow these steps:</span></span>

1. <span data-ttu-id="dcf79-203">No portal do Azure de Olá, navegue toohello conta do lote usada pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="dcf79-204">Em Olá **configurações** folha para a conta de lote hello, selecione **controle de acesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="dcf79-205">Clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="dcf79-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="dcf79-206">De saudação **função** lista suspensa, escolha a saudação _Colaborador_ ou _leitor_ função para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="dcf79-207">Para obter mais informações sobre essas funções, consulte [Introdução ao controle de acesso baseado em função no portal do Azure de saudação](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="dcf79-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="dcf79-208">Em Olá **selecione** , digite o nome de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="dcf79-209">Selecione o aplicativo hello lista e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="dcf79-210">O aplicativo agora deverá ser exibido nas configurações de controle de acesso com uma função RBAC atribuída.</span><span class="sxs-lookup"><span data-stu-id="dcf79-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Atribuir um aplicativo de tooyour função RBAC](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="dcf79-212">Obter ID de locatário Olá para Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="dcf79-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="dcf79-213">ID de locatário Olá identifica Olá locatário do AD Azure que fornece serviços de autenticação tooyour de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="dcf79-214">tooget Olá ID de locatário, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="dcf79-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="dcf79-215">No portal do Azure de Olá, selecione seu Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dcf79-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="dcf79-216">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="dcf79-216">Click **Properties**.</span></span>
3. <span data-ttu-id="dcf79-217">Copiar o valor GUID Olá fornecido para a ID de diretório hello.</span><span class="sxs-lookup"><span data-stu-id="dcf79-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="dcf79-218">Esse valor também é chamado de ID de locatário hello.</span><span class="sxs-lookup"><span data-stu-id="dcf79-218">This value is also called hello tenant ID.</span></span>

![Copiar a ID de diretório Olá](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="dcf79-220">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="dcf79-220">Code examples</span></span>

<span data-ttu-id="dcf79-221">exemplos de código de saudação nesta seção mostram como tooauthenticate com o AD do Azure usando a autenticação integrada e com uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="dcf79-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="dcf79-222">Esses exemplos de código usam o .NET, mas os conceitos de saudação são semelhantes para outros idiomas.</span><span class="sxs-lookup"><span data-stu-id="dcf79-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="dcf79-223">Um token de autenticação do AD do Azure expirará após uma hora.</span><span class="sxs-lookup"><span data-stu-id="dcf79-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="dcf79-224">Ao usar uma vida útil longa **BatchClient** do objeto, é recomendável que você recuperar um token de ADAL em cada solicitação tooensure sempre ter um token válido.</span><span class="sxs-lookup"><span data-stu-id="dcf79-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="dcf79-225">tooachieve isso no .NET, escrever um método que recupera Olá token do AD do Azure e passa esse método tooa **BatchTokenCredentials** objeto como um representante.</span><span class="sxs-lookup"><span data-stu-id="dcf79-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="dcf79-226">método de representante Hello é chamado em cada solicitação toohello lote serviço tooensure que é fornecido um token válido.</span><span class="sxs-lookup"><span data-stu-id="dcf79-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="dcf79-227">Por padrão ADAL armazena em cache os tokens, para que um novo token é recuperado do AD do Azure somente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="dcf79-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="dcf79-228">Para saber mais sobre tokens no AD do Azure, veja [Cenários de autenticação do AD do Azure][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="dcf79-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="dcf79-229">Exemplo de código: Usando a autenticação integrada do Azure AD com o .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="dcf79-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="dcf79-230">tooauthenticate com a autenticação integrada do .NET em lotes, Olá referência [do Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pacote e hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pacote.</span><span class="sxs-lookup"><span data-stu-id="dcf79-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="dcf79-231">Incluir o seguinte Olá `using` no seu código:</span><span class="sxs-lookup"><span data-stu-id="dcf79-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="dcf79-232">Saudação de referência ponto de extremidade do AD do Azure no seu código, incluindo Olá locatário ID.</span><span class="sxs-lookup"><span data-stu-id="dcf79-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="dcf79-233">tooretrieve Olá ID de locatário, siga etapas Olá descritas em [obter ID de locatário Olá para Active Directory do Azure](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="dcf79-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="dcf79-234">Referência de ponto de extremidade recurso serviço de lote de hello:</span><span class="sxs-lookup"><span data-stu-id="dcf79-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="dcf79-235">Referencie a conta do Lote:</span><span class="sxs-lookup"><span data-stu-id="dcf79-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="dcf79-236">Especifique a ID de aplicativo de saudação (ID do cliente) para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="dcf79-237">ID do aplicativo Hello está disponível em seu registro de aplicativo no portal do Azure de saudação:</span><span class="sxs-lookup"><span data-stu-id="dcf79-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="dcf79-238">Também copie o URI que você especificou durante o processo de registro de saudação de redirecionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="dcf79-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="dcf79-239">Olá URI especificado em seu código deve coincidir com a URI que você forneceu ao registrar o aplicativo hello de redirecionamento de saudação de redirecionamento:</span><span class="sxs-lookup"><span data-stu-id="dcf79-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="dcf79-240">Grave um token de autenticação do retorno de chamada método tooacquire saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf79-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="dcf79-241">Olá **GetAuthenticationTokenAsync** tooauthenticate ADAL as chamadas método de retorno de chamada mostrado aqui um usuário que está interagindo com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="dcf79-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="dcf79-242">Olá **AcquireTokenAsync** método fornecido por ADAL prompts Olá suas credenciais do usuário e o aplicativo hello continua uma vez usuário Olá fornecerá a eles (a menos que ele já tem em cache as credenciais):</span><span class="sxs-lookup"><span data-stu-id="dcf79-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="dcf79-243">Construir um **BatchTokenCredentials** objeto que usa Olá delegado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="dcf79-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="dcf79-244">Use essas credenciais tooopen um **BatchClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="dcf79-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="dcf79-245">Você pode usá-lo **BatchClient** objeto para operações subsequentes em relação a saudação serviço de lote:</span><span class="sxs-lookup"><span data-stu-id="dcf79-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="dcf79-246">Exemplo de código: Usando uma entidade de serviço do Azure AD com o .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="dcf79-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="dcf79-247">tooauthenticate com uma entidade de serviço do .NET em lotes, Olá referência [do Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pacote e hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pacote.</span><span class="sxs-lookup"><span data-stu-id="dcf79-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="dcf79-248">Incluir o seguinte Olá `using` no seu código:</span><span class="sxs-lookup"><span data-stu-id="dcf79-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="dcf79-249">Saudação de referência ponto de extremidade do AD do Azure no seu código, incluindo Olá locatário ID.</span><span class="sxs-lookup"><span data-stu-id="dcf79-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="dcf79-250">Ao usar uma entidade de serviço, você deve fornecer um ponto de extremidade específico ao locatário.</span><span class="sxs-lookup"><span data-stu-id="dcf79-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="dcf79-251">tooretrieve Olá ID de locatário, siga etapas Olá descritas em [obter ID de locatário Olá para Active Directory do Azure](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="dcf79-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="dcf79-252">Referência de ponto de extremidade recurso serviço de lote de hello:</span><span class="sxs-lookup"><span data-stu-id="dcf79-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="dcf79-253">Referencie a conta do Lote:</span><span class="sxs-lookup"><span data-stu-id="dcf79-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="dcf79-254">Especifique a ID de aplicativo de saudação (ID do cliente) para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dcf79-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="dcf79-255">ID do aplicativo Hello está disponível em seu registro de aplicativo no portal do Azure de saudação:</span><span class="sxs-lookup"><span data-stu-id="dcf79-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="dcf79-256">Especifique a chave de segredo Olá que você copiou da saudação portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="dcf79-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="dcf79-257">Grave um token de autenticação do retorno de chamada método tooacquire saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf79-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="dcf79-258">Olá **GetAuthenticationTokenAsync** método de retorno de chamada mostrado aqui chamadas de ADAL para autenticação autônoma:</span><span class="sxs-lookup"><span data-stu-id="dcf79-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="dcf79-259">Construir um **BatchTokenCredentials** objeto que usa Olá delegado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="dcf79-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="dcf79-260">Use essas credenciais tooopen um **BatchClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="dcf79-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="dcf79-261">Você pode usá-lo, em seguida, **BatchClient** objeto para operações subsequentes em relação a saudação serviço de lote:</span><span class="sxs-lookup"><span data-stu-id="dcf79-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="dcf79-262">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dcf79-262">Next steps</span></span>

<span data-ttu-id="dcf79-263">toolearn mais sobre o AD do Azure, consulte Olá [documentação do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="dcf79-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="dcf79-264">Os exemplos mais detalhados mostrando como toouse ADAL estão disponíveis no hello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="dcf79-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="dcf79-265">toolearn mais informações sobre entidades de serviço, consulte [objetos de aplicativo e serviço principal no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="dcf79-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="dcf79-266">toocreate uma entidade de serviço usando hello Azure portal, consulte [usar o aplicativo do portal toocreate do Active Directory e a entidade de serviço que pode acessar recursos](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dcf79-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="dcf79-267">Você também pode criar uma entidade de serviço com o PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf79-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="dcf79-268">aplicativos de gerenciamento de lote de tooauthenticate usando o AD do Azure, consulte [soluções de gerenciamento de lote de autenticar com o Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="dcf79-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "O que é o Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Cenários de autenticação do Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrando aplicativos com o Azure Active Directory"
[azure_portal]: http://portal.azure.com
