---
title: "Usar o Azure Active Directory para autenticar as soluções do serviço do Lote do Azure | Microsoft Docs"
description: "O Lote dá suporte ao Azure AD para autenticação por meio do serviço do Lote."
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
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="92aa5-103">Autenticar soluções do serviço do Lote no Active Directory</span><span class="sxs-lookup"><span data-stu-id="92aa5-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="92aa5-104">O Lote do Azure dá suporte à autenticação com o [Azure AD][aad_about] (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="92aa5-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="92aa5-105">O Azure AD é o serviço de gerenciamento de identidade e diretório multilocatário com base em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="92aa5-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="92aa5-106">O Azure em si usa o Azure AD para autenticar seus clientes, administradores de serviços e usuários organizacionais.</span><span class="sxs-lookup"><span data-stu-id="92aa5-106">Azure itself uses Azure AD to authenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="92aa5-107">Ao usar a autenticação do Azure AD com o Lote do Azure, você pode fazer a autenticação usando uma destas duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="92aa5-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="92aa5-108">Usando a **autenticação integrada** para autenticar um usuário que está interagindo com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-108">By using **integrated authentication** to authenticate a user that is interacting with the application.</span></span> <span data-ttu-id="92aa5-109">Um aplicativo que usa a autenticação integrada coleta as credenciais do usuário e usa essas credenciais para autenticar o acesso aos recursos do Lote.</span><span class="sxs-lookup"><span data-stu-id="92aa5-109">An application using integrated authentication gathers a user's credentials and uses those credentials to authenticate access to Batch resources.</span></span>
- <span data-ttu-id="92aa5-110">Usando uma **entidade de serviço** para autenticar um aplicativo autônomo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-110">By using a **service principal** to authenticate an unattended application.</span></span> <span data-ttu-id="92aa5-111">Uma entidade de serviço define a política e as permissões de um aplicativo, a fim de representar o aplicativo ao acessar recursos em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="92aa5-111">A service principal defines the policy and permissions for an application in order to represent the application when accessing resources at runtime.</span></span>

<span data-ttu-id="92aa5-112">Para saber mais sobre o Azure AD, veja a [documentação do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="92aa5-112">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="92aa5-113">Autenticação e modo de alocação de pool</span><span class="sxs-lookup"><span data-stu-id="92aa5-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="92aa5-114">Ao criar uma conta do Lote, você poderá especificar o local ao qual os pools criados para essa conta devem ser alocados.</span><span class="sxs-lookup"><span data-stu-id="92aa5-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="92aa5-115">Você pode optar por alocar pools na assinatura padrão do serviço do Lote ou em uma assinatura de usuário.</span><span class="sxs-lookup"><span data-stu-id="92aa5-115">You can choose to allocate pools either in the default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="92aa5-116">Sua escolha afeta como você autentica o acesso aos recursos nessa conta.</span><span class="sxs-lookup"><span data-stu-id="92aa5-116">Your choice affects how you authenticate access to resources in that account.</span></span>

- <span data-ttu-id="92aa5-117">**Assinatura do serviço do Lote**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-117">**Batch service subscription**.</span></span> <span data-ttu-id="92aa5-118">Por padrão, os pools de lote são alocados em uma assinatura de serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="92aa5-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="92aa5-119">Se você escolher essa opção, poderá autenticar o acesso aos recursos nessa conta com uma [Chave Compartilhada](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) ou com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92aa5-119">If you choose this option, you can authenticate access to resources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="92aa5-120">**Assinatura de usuário.**</span><span class="sxs-lookup"><span data-stu-id="92aa5-120">**User subscription.**</span></span> <span data-ttu-id="92aa5-121">Você pode optar por alocar pools do Lote em uma assinatura de usuário especificada.</span><span class="sxs-lookup"><span data-stu-id="92aa5-121">You can choose to allocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="92aa5-122">Se você escolher essa opção, deverá autenticar no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92aa5-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="92aa5-123">Pontos de extremidade para autenticação</span><span class="sxs-lookup"><span data-stu-id="92aa5-123">Endpoints for authentication</span></span>

<span data-ttu-id="92aa5-124">Para autenticar aplicativos do Lote no Azure AD, você precisa incluir alguns pontos de extremidade conhecidos no código.</span><span class="sxs-lookup"><span data-stu-id="92aa5-124">To authenticate Batch applications with Azure AD, you need to include some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="92aa5-125">Ponto de extremidade do Azure AD</span><span class="sxs-lookup"><span data-stu-id="92aa5-125">Azure AD endpoint</span></span>

<span data-ttu-id="92aa5-126">O ponto de extremidade de autoridade base do Azure AD é:</span><span class="sxs-lookup"><span data-stu-id="92aa5-126">The base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="92aa5-127">Para autenticar no Azure AD, use esse ponto de extremidade junto com a ID do locatário (ID do diretório).</span><span class="sxs-lookup"><span data-stu-id="92aa5-127">To authenticate with Azure AD, you use this endpoint together with the tenant ID (directory ID).</span></span> <span data-ttu-id="92aa5-128">A ID do locatário identifica o locatário do Azure AD a ser usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="92aa5-128">The tenant ID identifies the Azure AD tenant to use for authentication.</span></span> <span data-ttu-id="92aa5-129">Para recuperar a ID do locatário, siga as etapas descritas em [Obter a ID do locatário para o Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="92aa5-129">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="92aa5-130">O ponto de extremidade específico ao locatário é necessário quando você realiza uma autenticação usando uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="92aa5-130">The tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="92aa5-131">O ponto de extremidade específico ao locatário é opcional, mas recomendado, quando você realiza uma autenticação usando a autenticação integrada.</span><span class="sxs-lookup"><span data-stu-id="92aa5-131">The tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="92aa5-132">No entanto, você também pode usar o ponto de extremidade comum do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92aa5-132">However, you can also use the Azure AD common endpoint.</span></span> <span data-ttu-id="92aa5-133">O ponto de extremidade comum fornece uma interface genérica de coleta de credenciais quando um locatário específico não é fornecido.</span><span class="sxs-lookup"><span data-stu-id="92aa5-133">The common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="92aa5-134">O ponto de extremidade comum é `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="92aa5-134">The common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="92aa5-135">Para obter mais informações sobre pontos de extremidade do Azure AD, consulte [Cenários de autenticação do Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="92aa5-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="92aa5-136">Ponto de extremidade de recursos do Lote</span><span class="sxs-lookup"><span data-stu-id="92aa5-136">Batch resource endpoint</span></span>

<span data-ttu-id="92aa5-137">Use o **ponto de extremidade de recursos do Lote do Azure** para adquirir um token para autenticar solicitações no serviço do Lote:</span><span class="sxs-lookup"><span data-stu-id="92aa5-137">Use the **Azure Batch resource endpoint** to acquire a token for authenticating requests to the Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="92aa5-138">Registrar seu aplicativo em um locatário</span><span class="sxs-lookup"><span data-stu-id="92aa5-138">Register your application with a tenant</span></span>

<span data-ttu-id="92aa5-139">A primeira etapa do uso do Azure AD para realizar a autenticação é registrar seu aplicativo em um locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92aa5-139">The first step in using Azure AD to authenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="92aa5-140">O registro do aplicativo permite que você chame a [ADAL][aad_adal] (Biblioteca de Autenticação do Active Directory) do Azure por meio do código.</span><span class="sxs-lookup"><span data-stu-id="92aa5-140">Registering your application enables you to call the Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="92aa5-141">A ADAL fornece uma API para realizar a autenticação no Azure AD por meio do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-141">The ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="92aa5-142">O registro do aplicativo é necessário se você pretende usar a autenticação integrada ou uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="92aa5-142">Registering your application is required whether you plan to use integrated authentication or a service principal.</span></span>

<span data-ttu-id="92aa5-143">Ao registrar o aplicativo, você fornece informações sobre ele ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92aa5-143">When you register your application, you supply information about your application to Azure AD.</span></span> <span data-ttu-id="92aa5-144">Em seguida, o Azure AD fornece uma ID de aplicativo que você usa para associar seu aplicativo ao Azure AD em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="92aa5-144">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="92aa5-145">Para saber mais sobre a ID do aplicativo, veja [Objetos de aplicativo e de entidade de serviço no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="92aa5-145">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="92aa5-146">Para registrar o aplicativo Lote, siga as etapas da seção [Adicionar um aplicativo](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) em [Integração de aplicativos com o Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="92aa5-146">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="92aa5-147">Se você registrar o aplicativo como um Aplicativo Nativo, poderá especificar qualquer URI válido para o **URI de Redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-147">If you register your application as a Native Application, you can specify any valid URI for the **Redirect URI**.</span></span> <span data-ttu-id="92aa5-148">Ele não precisa ser um ponto de extremidade real.</span><span class="sxs-lookup"><span data-stu-id="92aa5-148">It does not need to be a real endpoint.</span></span>

<span data-ttu-id="92aa5-149">Depois de registrar o aplicativo, você verá a ID do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="92aa5-149">After you've registered your application, you'll see the application ID:</span></span>

![Registrar seu aplicativo Lote no Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="92aa5-151">Para obter mais informações sobre como registrar um aplicativo no Azure AD, consulte [Cenários de autenticação do Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="92aa5-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-the-tenant-id-for-your-active-directory"></a><span data-ttu-id="92aa5-152">Obter a ID do locatário para o Active Directory</span><span class="sxs-lookup"><span data-stu-id="92aa5-152">Get the tenant ID for your Active Directory</span></span>

<span data-ttu-id="92aa5-153">A ID do locatário identifica o locatário do Azure AD que fornece serviços de autenticação para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-153">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="92aa5-154">Para obter a ID de locatário, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="92aa5-154">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="92aa5-155">No portal do Azure, selecione seu Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92aa5-155">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="92aa5-156">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-156">Click **Properties**.</span></span>
3. <span data-ttu-id="92aa5-157">Copie o valor do GUID fornecido para a ID do diretório.</span><span class="sxs-lookup"><span data-stu-id="92aa5-157">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="92aa5-158">Esse valor também é chamado de ID do locatário.</span><span class="sxs-lookup"><span data-stu-id="92aa5-158">This value is also called the tenant ID.</span></span>

![Copiar a ID do diretório](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="92aa5-160">Usar a autenticação integrada</span><span class="sxs-lookup"><span data-stu-id="92aa5-160">Use integrated authentication</span></span>

<span data-ttu-id="92aa5-161">Para autenticar com a autenticação integrada, você precisa conceder as permissões do aplicativo para se conectar à API do serviço do Lote.</span><span class="sxs-lookup"><span data-stu-id="92aa5-161">To authenticate with integrated authentication, you need to grant your application permissions to connect to the Batch service API.</span></span> <span data-ttu-id="92aa5-162">Esta etapa permite que o aplicativo autentique chamadas à API do serviço do Lote no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92aa5-162">This step enables your application to authenticate calls to the Batch service API with Azure AD.</span></span>

<span data-ttu-id="92aa5-163">Depois de [registrar o aplicativo](#register-your-application-with-an-azure-ad-tenant), siga estas etapas no portal do Azure para conceder a ele o acesso ao serviço do Lote:</span><span class="sxs-lookup"><span data-stu-id="92aa5-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in the Azure portal to grant it access to the Batch service:</span></span>

1. <span data-ttu-id="92aa5-164">No painel de navegação esquerdo do portal do Azure, escolha **Mais Serviços** e clique em **Registros de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-164">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="92aa5-165">Pesquise pelo nome do seu aplicativo na lista de registros do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="92aa5-165">Search for the name of your application in the list of app registrations:</span></span>

    ![Procure o nome do aplicativo](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="92aa5-167">Abra a folha **Configurações** de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-167">Open the **Settings** blade for your application.</span></span> <span data-ttu-id="92aa5-168">Na seção **Acesso à API**, selecione **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-168">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="92aa5-169">No **permissões necessárias** folha, clique o **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="92aa5-169">In the **Required permissions** blade, click the **Add** button.</span></span>
5. <span data-ttu-id="92aa5-170">Na etapa 1, pesquise a API de Lote.</span><span class="sxs-lookup"><span data-stu-id="92aa5-170">In step 1, search for the Batch API.</span></span> <span data-ttu-id="92aa5-171">Procure cada uma dessas cadeias de caracteres até encontrar a API:</span><span class="sxs-lookup"><span data-stu-id="92aa5-171">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="92aa5-172">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="92aa5-173">**Lote do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="92aa5-174">Os locatários mais recentes do Azure AD podem usar esse nome.</span><span class="sxs-lookup"><span data-stu-id="92aa5-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="92aa5-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** é a ID para a API do Lote.</span><span class="sxs-lookup"><span data-stu-id="92aa5-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 
6. <span data-ttu-id="92aa5-176">Depois de encontrar a API de Lote, selecione-a e clique no botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-176">Once you find the Batch API, select it and click the **Select** button.</span></span>
6. <span data-ttu-id="92aa5-177">Na etapa 2, selecione a caixa de seleção Avançar ao **acesso serviço do Azure Batch** e clique no **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="92aa5-177">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
7. <span data-ttu-id="92aa5-178">Clique no botão **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-178">Click the **Done** button.</span></span>

<span data-ttu-id="92aa5-179">A folha **Permissões Necessárias** agora mostra que o aplicativo do Azure AD tem acesso à ADAL e à API do serviço do Lote.</span><span class="sxs-lookup"><span data-stu-id="92aa5-179">The **Required Permissions** blade now shows that your Azure AD application has access to both ADAL and the Batch service API.</span></span> <span data-ttu-id="92aa5-180">As permissões são concedidas à ADAL automaticamente quando você registra seu aplicativo no Azure AD pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="92aa5-180">Permissions are granted to ADAL automatically when you first register your app with Azure AD.</span></span>

![Conceder permissões de API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="92aa5-182">Usar uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="92aa5-182">Use a service principal</span></span> 

<span data-ttu-id="92aa5-183">Para autenticar um aplicativo que é executado de forma autônoma, use uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="92aa5-183">To authenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="92aa5-184">Depois de registrar o aplicativo, siga estas etapas no portal do Azure para configurar uma entidade de serviço:</span><span class="sxs-lookup"><span data-stu-id="92aa5-184">After you've registered your application, follow these steps in the Azure portal to configure a service principal:</span></span>

1. <span data-ttu-id="92aa5-185">Solicitar uma chave secreta para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="92aa5-186">Atribuir uma função RBAC ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-186">Assign an RBAC role to your application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="92aa5-187">Solicitar uma chave secreta para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="92aa5-187">Request a secret key for your application</span></span>

<span data-ttu-id="92aa5-188">Quando o aplicativo é autenticado com uma entidade de serviço, ele envia a ID do aplicativo e uma chave secreta para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92aa5-188">When your application authenticates with a service principal, it sends both the application ID and a secret key to Azure AD.</span></span> <span data-ttu-id="92aa5-189">Você precisará criar e copiar a chave secreta a ser usada do código.</span><span class="sxs-lookup"><span data-stu-id="92aa5-189">You'll need to create and copy the secret key to use from your code.</span></span>

<span data-ttu-id="92aa5-190">Siga estas etapas no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="92aa5-190">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="92aa5-191">No painel de navegação esquerdo do portal do Azure, escolha **Mais Serviços** e clique em **Registros de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-191">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="92aa5-192">Pesquise o nome do aplicativo na lista de registros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-192">Search for the name of your application in the list of app registrations.</span></span>
3. <span data-ttu-id="92aa5-193">Exibição de **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="92aa5-193">Display the **Settings** blade.</span></span> <span data-ttu-id="92aa5-194">Na seção **Acesso à API**, selecione **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-194">In the **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="92aa5-195">Para criar uma chave, insira uma descrição para a chave.</span><span class="sxs-lookup"><span data-stu-id="92aa5-195">To create a key, enter a description for the key.</span></span> <span data-ttu-id="92aa5-196">Em seguida, selecione uma duração para a chave de um ou dois anos.</span><span class="sxs-lookup"><span data-stu-id="92aa5-196">Then select a duration for the key of either one or two years.</span></span> 
5. <span data-ttu-id="92aa5-197">Clique no botão **Salvar** para criar e exibir a chave.</span><span class="sxs-lookup"><span data-stu-id="92aa5-197">Click the **Save** button to create and display the key.</span></span> <span data-ttu-id="92aa5-198">Copie o valor da chave para um local seguro, pois você não poderá acessá-lo novamente depois de sair da folha.</span><span class="sxs-lookup"><span data-stu-id="92aa5-198">Copy the key value to a safe place, as you won't be able to access it again after you leave the blade.</span></span> 

    ![Criar uma chave secreta](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a><span data-ttu-id="92aa5-200">Atribuir uma função RBAC ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="92aa5-200">Assign an RBAC role to your application</span></span>

<span data-ttu-id="92aa5-201">Para autenticar com uma entidade de serviço, você precisa atribuir uma função RBAC ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-201">To authenticate with a service principal, you need to assign an RBAC role to your application.</span></span> <span data-ttu-id="92aa5-202">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="92aa5-202">Follow these steps:</span></span>

1. <span data-ttu-id="92aa5-203">No portal do Azure, navegue para a conta do Lote usada pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-203">In the Azure portal, navigate to the Batch account used by your application.</span></span>
2. <span data-ttu-id="92aa5-204">Na folha **Configurações** da conta do Lote, selecione **Controle de Acesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-204">In the **Settings** blade for the Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="92aa5-205">Clique no botão **Adicionar** .</span><span class="sxs-lookup"><span data-stu-id="92aa5-205">Click the **Add** button.</span></span> 
4. <span data-ttu-id="92aa5-206">Na lista suspensa **Função**, escolha a função _Colaborador_ ou _Leitor_ para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-206">From the **Role** drop-down, choose either the _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="92aa5-207">Para obter mais informações sobre essas funções, consulte [Introdução ao Controle de Acesso Baseado em Função no portal do Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="92aa5-207">For more information on these roles, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="92aa5-208">No campo **Selecionar**, insira o nome de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-208">In the **Select** field, enter the name of your application.</span></span> <span data-ttu-id="92aa5-209">Selecione o aplicativo na lista e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-209">Select your application from the list, and click **Save**.</span></span>

<span data-ttu-id="92aa5-210">O aplicativo agora deverá ser exibido nas configurações de controle de acesso com uma função RBAC atribuída.</span><span class="sxs-lookup"><span data-stu-id="92aa5-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Atribuir uma função RBAC ao aplicativo](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="92aa5-212">Obter a ID do locatário para o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92aa5-212">Get the tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="92aa5-213">A ID do locatário identifica o locatário do Azure AD que fornece serviços de autenticação para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-213">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="92aa5-214">Para obter a ID de locatário, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="92aa5-214">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="92aa5-215">No portal do Azure, selecione seu Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92aa5-215">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="92aa5-216">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-216">Click **Properties**.</span></span>
3. <span data-ttu-id="92aa5-217">Copie o valor do GUID fornecido para a ID do diretório.</span><span class="sxs-lookup"><span data-stu-id="92aa5-217">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="92aa5-218">Esse valor também é chamado de ID do locatário.</span><span class="sxs-lookup"><span data-stu-id="92aa5-218">This value is also called the tenant ID.</span></span>

![Copiar a ID do diretório](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="92aa5-220">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="92aa5-220">Code examples</span></span>

<span data-ttu-id="92aa5-221">Os exemplos de código desta seção mostram como realizar a autenticação com o Azure AD usando a autenticação integrada e com uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="92aa5-221">The code examples in this section show how to authenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="92aa5-222">Esses exemplos de código usam o .NET, mas os conceitos são semelhantes para outras linguagens.</span><span class="sxs-lookup"><span data-stu-id="92aa5-222">These code examples use .NET, but the concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="92aa5-223">Um token de autenticação do AD do Azure expirará após uma hora.</span><span class="sxs-lookup"><span data-stu-id="92aa5-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="92aa5-224">Ao usar uma vida útil longa **BatchClient** de objeto, é recomendável que você recuperar um token da ADAL em cada solicitação para garantir que você sempre tenha um token válido.</span><span class="sxs-lookup"><span data-stu-id="92aa5-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="92aa5-225">Para fazer isso no .NET, escrever um método que recupera o token do AD do Azure e passar esse método para um **BatchTokenCredentials** objeto como um delegado.</span><span class="sxs-lookup"><span data-stu-id="92aa5-225">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="92aa5-226">O método de representante é chamado em cada solicitação para o serviço de lote para garantir que um token válido seja fornecido.</span><span class="sxs-lookup"><span data-stu-id="92aa5-226">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="92aa5-227">Por padrão ADAL armazena em cache os tokens, para que um novo token é recuperado do AD do Azure somente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="92aa5-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="92aa5-228">Para saber mais sobre tokens no AD do Azure, veja [Cenários de autenticação do AD do Azure][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="92aa5-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="92aa5-229">Exemplo de código: Usando a autenticação integrada do Azure AD com o .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="92aa5-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="92aa5-230">Para autenticar com a autenticação integrada por meio do .NET do Lote, referencie o pacote [.NET do Lote do Azure](https://www.nuget.org/packages/Azure.Batch/) e o pacote [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="92aa5-230">To authenticate with integrated authentication from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="92aa5-231">Inclua as seguintes intruções `using` no seu código:</span><span class="sxs-lookup"><span data-stu-id="92aa5-231">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="92aa5-232">Referencie o ponto de extremidade do Azure AD no código, incluindo a ID do locatário.</span><span class="sxs-lookup"><span data-stu-id="92aa5-232">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="92aa5-233">Para recuperar a ID do locatário, siga as etapas descritas em [Obter a ID do locatário para o Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="92aa5-233">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="92aa5-234">Referencie o ponto de extremidade de recursos do serviço do Lote:</span><span class="sxs-lookup"><span data-stu-id="92aa5-234">Reference the Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="92aa5-235">Referencie a conta do Lote:</span><span class="sxs-lookup"><span data-stu-id="92aa5-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="92aa5-236">Especifique a ID do aplicativo (ID do cliente) para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-236">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="92aa5-237">A ID do aplicativo está disponível no registro de aplicativo no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="92aa5-237">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="92aa5-238">Também copie o URI que você especificou durante o processo de registro de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="92aa5-238">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="92aa5-239">O URI de redirecionamento especificado no código deve corresponder ao URI de redirecionamento que você forneceu quando registrou o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="92aa5-239">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="92aa5-240">Escreva um método de retorno de chamada para adquirir o token de autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="92aa5-240">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="92aa5-241">O método de retorno de chamada **GetAuthenticationTokenAsync** mostrado aqui chama a ADAL para autenticar um usuário que está interagindo com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-241">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL to authenticate a user who is interacting with the application.</span></span> <span data-ttu-id="92aa5-242">O método **AcquireTokenAsync** fornecido pela ADAL solicita ao usuário suas credenciais e o aplicativo continua depois que o usuário fornece essas credenciais (a menos que ele já tenha as credenciais armazenadas em cache):</span><span class="sxs-lookup"><span data-stu-id="92aa5-242">The **AcquireTokenAsync** method provided by ADAL prompts the user for their credentials, and the application proceeds once the user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="92aa5-243">Construa um objeto **BatchTokenCredentials** que use o delegado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="92aa5-243">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="92aa5-244">Use essas credenciais para abrir um objeto **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-244">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="92aa5-245">Você pode usar esse objeto **BatchClient** para as próximas operações no serviço do Lote:</span><span class="sxs-lookup"><span data-stu-id="92aa5-245">You can use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="92aa5-246">Exemplo de código: Usando uma entidade de serviço do Azure AD com o .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="92aa5-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="92aa5-247">Para autenticar com uma entidade de serviço por meio do .NET do Lote, referencie o pacote [.NET do Lote do Azure](https://www.nuget.org/packages/Azure.Batch/) e o pacote [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="92aa5-247">To authenticate with a service principal from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="92aa5-248">Inclua as seguintes intruções `using` no seu código:</span><span class="sxs-lookup"><span data-stu-id="92aa5-248">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="92aa5-249">Referencie o ponto de extremidade do Azure AD no código, incluindo a ID do locatário.</span><span class="sxs-lookup"><span data-stu-id="92aa5-249">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="92aa5-250">Ao usar uma entidade de serviço, você deve fornecer um ponto de extremidade específico ao locatário.</span><span class="sxs-lookup"><span data-stu-id="92aa5-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="92aa5-251">Para recuperar a ID do locatário, siga as etapas descritas em [Obter a ID do locatário para o Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="92aa5-251">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="92aa5-252">Referencie o ponto de extremidade de recursos do serviço do Lote:</span><span class="sxs-lookup"><span data-stu-id="92aa5-252">Reference the Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="92aa5-253">Referencie a conta do Lote:</span><span class="sxs-lookup"><span data-stu-id="92aa5-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="92aa5-254">Especifique a ID do aplicativo (ID do cliente) para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92aa5-254">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="92aa5-255">A ID do aplicativo está disponível no registro de aplicativo no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="92aa5-255">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="92aa5-256">Especifique a chave secreta que você copiou do portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="92aa5-256">Specify the secret key that you copied from the Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="92aa5-257">Escreva um método de retorno de chamada para adquirir o token de autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="92aa5-257">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="92aa5-258">O método de retorno de chamada **GetAuthenticationTokenAsync** mostrado aqui chama a ADAL para a autenticação autônoma:</span><span class="sxs-lookup"><span data-stu-id="92aa5-258">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="92aa5-259">Construa um objeto **BatchTokenCredentials** que use o delegado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="92aa5-259">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="92aa5-260">Use essas credenciais para abrir um objeto **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="92aa5-260">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="92aa5-261">Depois, você pode usar esse objeto **BatchClient** para as próximas operações no serviço do Lote:</span><span class="sxs-lookup"><span data-stu-id="92aa5-261">You can then use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="92aa5-262">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92aa5-262">Next steps</span></span>

<span data-ttu-id="92aa5-263">Para saber mais sobre o Azure AD, veja a [documentação do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="92aa5-263">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="92aa5-264">Exemplos mais detalhados que mostram como usar o ADAL estão disponíveis na biblioteca [Amostras de código do Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="92aa5-264">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="92aa5-265">Para saber mais sobre entidades de serviço, consulte [Objetos de aplicativo e de entidade de serviço no Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="92aa5-265">To learn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="92aa5-266">Para criar uma entidade de serviço usando o portal do Azure, consulte [Usar o portal para criar um aplicativo e uma entidade de serviço do Active Directory que pode acessar recursos](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="92aa5-266">To create a service principal using the Azure portal, see [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="92aa5-267">Você também pode criar uma entidade de serviço com o PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="92aa5-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="92aa5-268">Para autenticar aplicativos do Gerenciamento de Lotes usando o Azure AD, consulte [Autenticar soluções do Gerenciamento de Lotes de com o Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="92aa5-268">To authenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

<span data-ttu-id="92aa5-269">[aad_about]: ../active-directory/active-directory-whatis.md "O que é o Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="92aa5-269">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="92aa5-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Cenários de autenticação do Azure AD"</span><span class="sxs-lookup"><span data-stu-id="92aa5-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="92aa5-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrando aplicativos com o Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="92aa5-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[azure_portal]: http://portal.azure.com
