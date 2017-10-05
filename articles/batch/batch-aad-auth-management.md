---
title: "Usar o Azure Active Directory para autenticar as soluções de gerenciamento do lote | Microsoft Docs"
description: Aplicativos criados com o Azure Resource Manager e o provedor de recursos de lote se autenticam com o Azure AD.
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
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="953fb-103">Autenticar soluções de gerenciamento do lote com o Active Directory</span><span class="sxs-lookup"><span data-stu-id="953fb-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="953fb-104">Aplicativos que chamam o serviço Azure Batch Management se autenticam com [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="953fb-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="953fb-105">O Azure AD é o serviço de gerenciamento de identidade e diretório multilocatário com base em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="953fb-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="953fb-106">O Azure em si usa o AD do Azure (Active Directory do Azure) para a autenticação de seus clientes, administradores de serviços e usuários organizacionais.</span><span class="sxs-lookup"><span data-stu-id="953fb-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="953fb-107">A biblioteca .NET do Gerenciamento do Lote expõe os tipos para trabalhar com contas, chaves de conta, aplicativos e pacotes de aplicativos do Lote.</span><span class="sxs-lookup"><span data-stu-id="953fb-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="953fb-108">A biblioteca .NET do Gerenciamento do Lote é um cliente do provedor de recursos do Azure e é usada junto com o [Azure Resource Manager][resman_overview] para gerenciar esses recursos por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="953fb-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="953fb-109">O Azure AD é necessário para autenticar solicitações feitas por meio de qualquer cliente de provedor de recursos do Azure, incluindo a biblioteca .NET do Gerenciamento do Lote e por meio do [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="953fb-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="953fb-110">Neste artigo, exploraremos como usar o Azure AD para autenticar aplicativos que usem a biblioteca do Batch Management .NET.</span><span class="sxs-lookup"><span data-stu-id="953fb-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="953fb-111">Mostramos como usar o Azure AD para autenticar um administrador ou coadministrador de assinatura usando a autenticação integrada.</span><span class="sxs-lookup"><span data-stu-id="953fb-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="953fb-112">Nesta seção, usamos o projeto de exemplo [AccountManagment][acct_mgmt_sample], disponível no GitHub, para percorrer o uso do Azure AD com a biblioteca do Batch Management .NET.</span><span class="sxs-lookup"><span data-stu-id="953fb-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="953fb-113">Para saber mais sobre como usar a biblioteca .NET do Gerenciamento do Lote e o exemplo AccountManagement, veja [Gerenciar contas e cotas do Lote com a biblioteca de cliente do Gerenciamento do Lote para .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="953fb-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="953fb-114">Registrar seu aplicativo no Azure AD</span><span class="sxs-lookup"><span data-stu-id="953fb-114">Register your application with Azure AD</span></span>

<span data-ttu-id="953fb-115">A ADAL [Biblioteca de Autenticação do Active Directory][aad_adal] fornece uma interface programática para o Azure AD para uso em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="953fb-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="953fb-116">Para chamar a ADAL de seu aplicativo, você deve registrar seu aplicativo em um locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="953fb-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="953fb-117">Quando você registra seu aplicativo, fornece ao Azure AD informações sobre seu aplicativo, incluindo um nome para ele dentro do locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="953fb-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="953fb-118">Em seguida, o Azure AD fornece uma ID de aplicativo que você usa para associar seu aplicativo ao Azure AD em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="953fb-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="953fb-119">Para saber mais sobre a ID do aplicativo, veja [Objetos de aplicativo e de entidade de serviço no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="953fb-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="953fb-120">Para registrar o aplicativo de exemplo AccountManagement, siga as etapas da seção [Adição de um aplicativo](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) em [Integração de aplicativos ao Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="953fb-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="953fb-121">Especifique **aplicativo cliente nativo** para o tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="953fb-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="953fb-122">O URI do OAuth 2.0 padrão do setor para o **URI de Redirecionamento** é `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="953fb-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="953fb-123">Porém, você pode especificar qualquer URI válido (como `http://myaccountmanagementsample`) para o **URI de Redirecionamento**, pois ele não precisa ser um ponto de extremidade real:</span><span class="sxs-lookup"><span data-stu-id="953fb-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="953fb-124">Depois de concluir o processo de registro, você verá a ID do aplicativo e a ID de objeto (entidade de serviço) listados para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="953fb-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="953fb-125">Conceder à API do Azure Resource Manager acesso a seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="953fb-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="953fb-126">Em seguida, você precisará delegar o acesso ao seu aplicativo para a API do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="953fb-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="953fb-127">O identificador do Azure AD para a API do Resource Manager é **API de Gerenciamento de Serviços do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="953fb-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="953fb-128">Siga estas etapas no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="953fb-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="953fb-129">No painel de navegação à esquerda do portal do Azure, escolha **Mais Serviços**, clique em **Registros de Aplicativo** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="953fb-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="953fb-130">Pesquise pelo nome do seu aplicativo na lista de registros do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="953fb-130">Search for the name of your application in the list of app registrations:</span></span>

    ![Procure o nome do aplicativo](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="953fb-132">Exibição de **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="953fb-132">Display the **Settings** blade.</span></span> <span data-ttu-id="953fb-133">Na seção **Acesso à API**, selecione **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="953fb-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="953fb-134">Clique em **adicionar** para adicionar uma nova permissão necessária.</span><span class="sxs-lookup"><span data-stu-id="953fb-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="953fb-135">Na etapa 1, digite **API de gerenciamento de serviços do Microsoft Azure**, selecione essa API da lista de resultados e clique no **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="953fb-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="953fb-136">Na etapa 2, selecione a caixa de seleção Avançar ao **Aceder a modelo de implantação clássico do Azure enquanto usuários da organização**e clique no **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="953fb-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="953fb-137">Clique no botão **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="953fb-137">Click the **Done** button.</span></span>

<span data-ttu-id="953fb-138">O **permissões necessárias** folha agora mostra que as permissões para o seu aplicativo são concedidas ao ADAL e APIs do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="953fb-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="953fb-139">Permissões são concedidas a ADAL por padrão, quando você primeiro registra seu aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="953fb-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Delegar permissões para a API do Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="953fb-141">Pontos de extremidade do Azure AD</span><span class="sxs-lookup"><span data-stu-id="953fb-141">Azure AD endpoints</span></span>

<span data-ttu-id="953fb-142">Para autenticar suas soluções de gerenciamento do lote com o Azure AD, você precisará de dois pontos de extremidade conhecidos.</span><span class="sxs-lookup"><span data-stu-id="953fb-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="953fb-143">O **ponto de extremidade comum do Azure AD** fornece uma interface de coleta de credenciais genérica quando um locatário específico não é fornecido, como no caso de autenticação integrada:</span><span class="sxs-lookup"><span data-stu-id="953fb-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="953fb-144">O **ponto de extremidade do Azure Resource Manager** é usado para adquirir um token para autenticar solicitações no serviço de gerenciamento do lote:</span><span class="sxs-lookup"><span data-stu-id="953fb-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="953fb-145">O aplicativo de exemplo AccountManagement define constantes para esses pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="953fb-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="953fb-146">Deixe essas constantes inalterados:</span><span class="sxs-lookup"><span data-stu-id="953fb-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="953fb-147">Consultar a ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="953fb-147">Reference your application ID</span></span> 

<span data-ttu-id="953fb-148">O aplicativo cliente usa a ID do aplicativo (também conhecida como a ID do cliente) para acessar o Azure AD em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="953fb-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="953fb-149">Depois de registrar seu aplicativo no portal do Azure, atualize seu código para usar a ID do aplicativo fornecida pelo Azure AD para seu aplicativo registrado.</span><span class="sxs-lookup"><span data-stu-id="953fb-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="953fb-150">No aplicativo de exemplo de AccountManagement, copie a ID do aplicativo do portal do Azure à constante apropriada:</span><span class="sxs-lookup"><span data-stu-id="953fb-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="953fb-151">Também copie o URI que você especificou durante o processo de registro de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="953fb-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="953fb-152">O URI de redirecionamento especificado no código deve corresponder ao URI de redirecionamento que você forneceu quando registrou o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="953fb-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="953fb-153">Adquirir um token de autenticação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="953fb-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="953fb-154">Depois de registrar o exemplo AccountManagement no locatário do Azure AD e de atualizar o código-fonte de exemplo com os valores, o exemplo estará pronto para se autenticar usando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="953fb-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="953fb-155">Quando você executar o exemplo, o ADAL tenta adquirir um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="953fb-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="953fb-156">Nesta etapa, ele solicitará suas credenciais da Microsoft:</span><span class="sxs-lookup"><span data-stu-id="953fb-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="953fb-157">Depois de fornecer suas credenciais, o aplicativo de exemplo poderá emitir solicitações autenticadas para o serviço de Gerenciamento do Lote.</span><span class="sxs-lookup"><span data-stu-id="953fb-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="953fb-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="953fb-158">Next steps</span></span>

<span data-ttu-id="953fb-159">Para saber mais sobre a execução do [aplicativo de exemplo AccountManagement][acct_mgmt_sample], veja [Gerenciar contas e cotas do Lote com a biblioteca de cliente de Gerenciamento do Lote para .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="953fb-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="953fb-160">Para saber mais sobre o Azure AD, veja a [documentação do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="953fb-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="953fb-161">Exemplos mais detalhados que mostram como usar o ADAL estão disponíveis na biblioteca [Amostras de código do Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="953fb-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="953fb-162">Para autenticar aplicativos de serviço do lote usando o Azure AD, consulte [Autenticar soluções de serviço do lote no Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="953fb-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="953fb-163">[aad_about]: ../active-directory/active-directory-whatis.md "O que é o Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="953fb-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="953fb-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Cenários de autenticação do Azure AD"</span><span class="sxs-lookup"><span data-stu-id="953fb-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="953fb-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrando aplicativos com o Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="953fb-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
