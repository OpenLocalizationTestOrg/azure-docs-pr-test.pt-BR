---
title: "soluções de gerenciamento de lote de tooauthenticate aaaUse Active Directory do Azure | Microsoft Docs"
description: "Aplicativos criados com o Gerenciador de recursos do Azure e o provedor de recursos de lote Olá autenticar com o AD do Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="95447-103">Autenticar soluções de gerenciamento do lote com o Active Directory</span><span class="sxs-lookup"><span data-stu-id="95447-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="95447-104">Aplicativos que chamam o serviço de gerenciamento do Azure em lote Olá autenticam com [Active Directory do Azure] [ aad_about] (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="95447-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="95447-105">O Azure AD é o serviço de gerenciamento de identidade e diretório multilocatário com base em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="95447-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="95447-106">Azure próprio usa o Azure AD para autenticação de saudação de seus clientes, os administradores de serviços e usuários organizacionais.</span><span class="sxs-lookup"><span data-stu-id="95447-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="95447-107">biblioteca de Batch Management .NET Olá expõe tipos para trabalhar com contas em lotes, as chaves de conta, aplicativos e pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="95447-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="95447-108">biblioteca do Hello Batch Management .NET é um cliente do provedor de recursos do Azure e é usada junto com [do Azure Resource Manager] [ resman_overview] toomanage esses recursos por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="95447-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="95447-109">AD do Azure é necessário tooauthenticate solicitações feitas por meio de qualquer cliente de provedor de recursos do Azure, incluindo a biblioteca de Batch Management .NET Olá e [do Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="95447-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="95447-110">Neste artigo, vamos explorar usando tooauthenticate do AD do Azure de aplicativos que usam a biblioteca de Batch Management .NET hello.</span><span class="sxs-lookup"><span data-stu-id="95447-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="95447-111">Vamos mostrar como toouse AD do Azure tooauthenticate um administrador de assinatura ou coadministrador, usando autenticação integrada.</span><span class="sxs-lookup"><span data-stu-id="95447-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="95447-112">Usamos Olá [AccountManagment] [ acct_mgmt_sample] projeto de exemplo, disponível no GitHub, toowalk por meio do usando o AD do Azure com biblioteca de Batch Management .NET hello.</span><span class="sxs-lookup"><span data-stu-id="95447-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="95447-113">toolearn mais sobre como usar a biblioteca de Batch Management .NET hello e exemplo de AccountManagement hello, consulte [cotas com biblioteca de cliente de gerenciamento em lote Olá para .NET e contas em lotes gerenciar](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="95447-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="95447-114">Registrar seu aplicativo no Azure AD</span><span class="sxs-lookup"><span data-stu-id="95447-114">Register your application with Azure AD</span></span>

<span data-ttu-id="95447-115">Hello Azure [biblioteca de autenticação do Active Directory] [ aad_adal] (ADAL) fornece uma interface programática de tooAzure AD para uso em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="95447-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="95447-116">toocall ADAL do seu aplicativo, você deve registrar seu aplicativo em um locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="95447-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="95447-117">Quando você registra seu aplicativo, você fornecer AD do Azure com informações sobre seu aplicativo, incluindo um nome para ele no locatário do AD do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="95447-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="95447-118">Em seguida, o AD do Azure fornece uma ID de aplicativo que você use tooassociate seu aplicativo com o AD do Azure em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="95447-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="95447-119">toolearn mais informações sobre a ID do aplicativo hello, consulte [objetos de aplicativo e serviço principal no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="95447-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="95447-120">Olá tooregister AccountManagement aplicativo de exemplo, siga as etapas de Olá Olá [adicionar um aplicativo](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) seção [integrando aplicativos com o Active Directory do Azure] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="95447-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="95447-121">Especifique **aplicativo cliente nativo** para o tipo de saudação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95447-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="95447-122">Olá setor URI de OAuth 2.0 padrão para Olá **URI de redirecionamento** é `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="95447-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="95447-123">No entanto, você pode especificar qualquer URI válido (como `http://myaccountmanagementsample`) para Olá **URI de redirecionamento**, pois ele não precisa toobe um ponto de extremidade real:</span><span class="sxs-lookup"><span data-stu-id="95447-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="95447-124">Depois de concluir o processo de registro Olá, você ver a ID do aplicativo hello e Olá ID de objeto (entidade de serviço) listado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95447-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="95447-125">Conceder ao aplicativo de tooyour de acesso de API do Gerenciador de recursos do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="95447-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="95447-126">Em seguida, você precisará toodelegate acesso tooyour aplicativo toohello API do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="95447-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="95447-127">Identificador de saudação do AD do Azure para Olá API do Gerenciador de recursos é **API de gerenciamento de serviço do Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="95447-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="95447-128">Siga estas etapas no hello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="95447-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="95447-129">No painel de navegação do lado esquerdo de saudação do Olá portal do Azure, escolha **mais serviços**, clique em **registros do aplicativo**e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="95447-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="95447-130">Pesquisar por nome de saudação do seu aplicativo na lista de saudação de registros do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="95447-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Procure o nome do aplicativo](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="95447-132">Saudação de exibição **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="95447-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="95447-133">Em Olá **acesso à API** seção, selecione **as permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="95447-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="95447-134">Clique em **adicionar** tooadd uma nova permissão necessária.</span><span class="sxs-lookup"><span data-stu-id="95447-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="95447-135">Na etapa 1, digite **API de gerenciamento de serviço do Windows Azure**, selecione essa API Olá lista de resultados e clique Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="95447-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="95447-136">Na etapa 2, selecione Olá caixa de seleção próxima muito**modelo de implantação clássico do Azure de acesso como usuários da organização**e clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="95447-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="95447-137">Clique em Olá **feito** botão.</span><span class="sxs-lookup"><span data-stu-id="95447-137">Click hello **Done** button.</span></span>

<span data-ttu-id="95447-138">Olá **permissões necessárias** folha agora mostra que o aplicativo de tooyour permissões são concedidas tooboth Olá ADAL e APIs do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="95447-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="95447-139">Permissões são concedidas tooADAL por padrão, quando você primeiro registra seu aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95447-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![Delegar permissões toohello API do Gerenciador de recursos do Azure](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="95447-141">Pontos de extremidade do Azure AD</span><span class="sxs-lookup"><span data-stu-id="95447-141">Azure AD endpoints</span></span>

<span data-ttu-id="95447-142">tooauthenticate suas soluções de gerenciamento em lote com o AD do Azure, você precisará de dois pontos de extremidade bem conhecidos.</span><span class="sxs-lookup"><span data-stu-id="95447-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="95447-143">Olá **ponto de extremidade comum do AD do Azure** fornece uma credencial genérica coletar interface quando um locatário específico não for fornecido, como no caso de saudação da autenticação integrada do:</span><span class="sxs-lookup"><span data-stu-id="95447-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="95447-144">Olá **ponto de extremidade do Azure Resource Manager** é tooacquire usado um token para autenticar o serviço de gerenciamento de lote de toohello solicitações:</span><span class="sxs-lookup"><span data-stu-id="95447-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="95447-145">Olá AccountManagement aplicativo de exemplo define constantes para esses pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="95447-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="95447-146">Deixe essas constantes inalterados:</span><span class="sxs-lookup"><span data-stu-id="95447-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="95447-147">Consultar a ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="95447-147">Reference your application ID</span></span> 

<span data-ttu-id="95447-148">O aplicativo cliente usa Olá aplicativo ID (também chamado tooas Olá ID do cliente) tooaccess AD do Azure em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="95447-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="95447-149">Depois de registrar seu aplicativo no portal do Azure de saudação, atualize sua ID de aplicativo do código toouse Olá fornecido pelo AD do Azure para seu aplicativo registrado.</span><span class="sxs-lookup"><span data-stu-id="95447-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="95447-150">Em Olá AccountManagement aplicativo de exemplo, copie a ID do aplicativo de constante apropriada do hello toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="95447-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="95447-151">Também copie o URI que você especificou durante o processo de registro de saudação de redirecionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="95447-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="95447-152">Olá redirecionar URI especificado em seu código deve coincidir com a URI que você forneceu ao registrar o aplicativo hello de redirecionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="95447-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="95447-153">Adquirir um token de autenticação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="95447-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="95447-154">Depois que você registrar o exemplo de AccountManagement hello no locatário do AD do Azure hello e atualize o código-fonte exemplo hello com seus valores, o exemplo hello é pronto tooauthenticate usando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95447-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="95447-155">Quando você executar o exemplo hello, Olá ADAL tenta tooacquire um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="95447-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="95447-156">Nesta etapa, ele solicitará suas credenciais da Microsoft:</span><span class="sxs-lookup"><span data-stu-id="95447-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="95447-157">Depois de fornecer suas credenciais, o aplicativo de exemplo hello poderá tooissue autenticado solicitações toohello serviço de gerenciamento de lote.</span><span class="sxs-lookup"><span data-stu-id="95447-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="95447-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="95447-158">Next steps</span></span>

<span data-ttu-id="95447-159">Para obter mais informações sobre como executar Olá [aplicativo de exemplo AccountManagement][acct_mgmt_sample], consulte [contas de lote de gerenciar e cotas com biblioteca de cliente de gerenciamento em lote Olá para .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="95447-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="95447-160">toolearn mais sobre o AD do Azure, consulte Olá [documentação do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="95447-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="95447-161">Os exemplos mais detalhados mostrando como toouse ADAL estão disponíveis no hello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="95447-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="95447-162">aplicativos de serviço de lote tooauthenticate usando o AD do Azure, consulte [soluções de serviço de lote autenticar com o Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="95447-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "O que é o Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Cenários de autenticação do Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrando aplicativos com o Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
