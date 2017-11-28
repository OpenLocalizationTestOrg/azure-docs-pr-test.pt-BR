---
title: "recursos da conta de lote aaaManage com biblioteca de saudação do cliente para .NET - Azure | Microsoft Docs"
description: Criar, excluir e modificar recursos da conta de lote do Azure com biblioteca de Batch Management .NET hello.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a><span data-ttu-id="4fa28-103">Gerenciar contas de lote e cotas com biblioteca de cliente de gerenciamento em lote Olá para .NET</span><span class="sxs-lookup"><span data-stu-id="4fa28-103">Manage Batch accounts and quotas with hello Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fa28-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa28-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="4fa28-105">.NET de Gerenciamento do Lote</span><span class="sxs-lookup"><span data-stu-id="4fa28-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="4fa28-106">Você pode diminuir manutenção sobrecarga em seus aplicativos de lote do Azure usando Olá [Batch Management .NET] [ api_mgmt_net] criação de conta do lote de tooautomate de biblioteca, exclusão, gerenciamento de chaves e descoberta de cota.</span><span class="sxs-lookup"><span data-stu-id="4fa28-106">You can lower maintenance overhead in your Azure Batch applications by using hello [Batch Management .NET][api_mgmt_net] library tooautomate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="4fa28-107">**Criar e excluir contas do Lote** em qualquer região.</span><span class="sxs-lookup"><span data-stu-id="4fa28-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="4fa28-108">Se, por exemplo, como um fornecedor de software independente (ISV) fornece um serviço para clientes em que cada um é atribuída a uma conta de lote separada para fins de cobrança, você pode adicionar conta criação e exclusão recursos tooyour portal do cliente.</span><span class="sxs-lookup"><span data-stu-id="4fa28-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities tooyour customer portal.</span></span>
* <span data-ttu-id="4fa28-109">**Recuperar e regenerar chaves de conta** programaticamente para qualquer uma de suas contas do Lote.</span><span class="sxs-lookup"><span data-stu-id="4fa28-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="4fa28-110">Isso pode ajudá-lo a atender às políticas de segurança que impõem substituição periódica ou expiração de chaves de conta.</span><span class="sxs-lookup"><span data-stu-id="4fa28-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="4fa28-111">Quando você tiver várias contas do Lote em várias regiões do Azure, a automação desse processo de substituição aumentará a eficiência da solução.</span><span class="sxs-lookup"><span data-stu-id="4fa28-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="4fa28-112">**Verifique as cotas de conta** e tomar Olá tentativa e erro suposições determinando quais contas de lote tem que limites.</span><span class="sxs-lookup"><span data-stu-id="4fa28-112">**Check account quotas** and take hello trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="4fa28-113">Ao verificar suas cotas de conta antes de iniciar trabalhos, de criar pools ou de adicionar nós de computação, você poderá ajustar proativamente quando ou onde esses recursos de computação serão criados.</span><span class="sxs-lookup"><span data-stu-id="4fa28-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="4fa28-114">Você pode determinar quais contas exigem aumento de cota antes da alocação de recursos adicionais a elas.</span><span class="sxs-lookup"><span data-stu-id="4fa28-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="4fa28-115">**Combine recursos de outros serviços do Azure** para uma experiência de gerenciamento completo – usando o Batch Management .NET, [Active Directory do Azure][aad_about]e hello [Azure Gerenciador de recursos de] [ resman_overview] juntos em Olá mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4fa28-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and hello [Azure Resource Manager][resman_overview] together in hello same application.</span></span> <span data-ttu-id="4fa28-116">Usando esses recursos e suas APIs, fornecer uma experiência de autenticação ininterrupto, Olá toocreate de capacidade e excluir grupos de recursos e capacidades de saudação descritos acima para uma solução de gerenciamento de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="4fa28-116">By using these features and their APIs, you can provide a frictionless authentication experience, hello ability toocreate and delete resource groups, and hello capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="4fa28-117">Enquanto este artigo enfoca o gerenciamento programático de saudação de suas contas, chaves e cotas do lote, você pode executar muitas dessas atividades usando Olá [portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="4fa28-117">While this article focuses on hello programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="4fa28-118">Para obter mais informações, consulte [criar uma conta de lote do Azure usando o portal do Azure de saudação](batch-account-create-portal.md) e [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="4fa28-118">For more information, see [Create an Azure Batch account using hello Azure portal](batch-account-create-portal.md) and [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="4fa28-119">Criar e excluir contas do Lote</span><span class="sxs-lookup"><span data-stu-id="4fa28-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="4fa28-120">Conforme mencionado, um dos principais recursos de saudação do hello API de gerenciamento do lote é toocreate e excluir contas de lote em uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa28-120">As mentioned, one of hello primary features of hello Batch Management API is toocreate and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="4fa28-121">Assim, use toodo [BatchManagementClient.Account.CreateAsync] [ net_create] e [DeleteAsync][net_delete], ou suas contrapartes síncronas.</span><span class="sxs-lookup"><span data-stu-id="4fa28-121">toodo so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="4fa28-122">Hello trecho de código a seguir cria uma conta, obtém Olá recentemente criado a conta de serviço de lote de saudação e, em seguida, exclui-lo.</span><span class="sxs-lookup"><span data-stu-id="4fa28-122">hello following code snippet creates an account, obtains hello newly created account from hello Batch service, and then deletes it.</span></span> <span data-ttu-id="4fa28-123">Neste trecho e Olá outros neste artigo, `batchManagementClient` é uma instância completamente inicializada de [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="4fa28-123">In this snippet and hello others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="4fa28-124">Aplicativos que usam a biblioteca de Batch Management .NET hello e sua classe BatchManagementClient precisam **administrador de serviço** ou **coadministrator** acessar toohello assinatura que possui Olá Conta de lote toobe gerenciado.</span><span class="sxs-lookup"><span data-stu-id="4fa28-124">Applications that use hello Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access toohello subscription that owns hello Batch account toobe managed.</span></span> <span data-ttu-id="4fa28-125">Para obter mais informações, consulte Olá [Active Directory do Azure](#azure-active-directory) seção e hello [AccountManagement] [ acct_mgmt_sample] exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="4fa28-125">For more information, see hello [Azure Active Directory](#azure-active-directory) section and hello [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="4fa28-126">Recuperar e regenerar chaves de conta</span><span class="sxs-lookup"><span data-stu-id="4fa28-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="4fa28-127">Obtenha as chaves da conta principal e secundária de qualquer conta do Lote em sua assinatura usando [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="4fa28-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="4fa28-128">É possível regenerar essas chaves usando [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="4fa28-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="4fa28-129">Você pode criar um fluxo de trabalho simplificado de conexão para os aplicativos de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="4fa28-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="4fa28-130">Primeiro, obtenha uma chave de conta para conta do lote Olá desejar toomanage com [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="4fa28-130">First, obtain an account key for hello Batch account you wish toomanage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="4fa28-131">Em seguida, usar essa chave durante a inicialização da biblioteca do .NET em lotes Olá [BatchSharedKeyCredentials] [ net_sharedkeycred] classe, que é usado ao inicializar [BatchClient] [net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="4fa28-131">Then, use this key when initializing hello Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="4fa28-132">Verificar a assinatura e cotas da conta do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="4fa28-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="4fa28-133">As assinaturas do Azure e Olá serviços individuais do Azure como lote todos têm cotas padrão que limitam o número de saudação de determinadas entidades dentro deles.</span><span class="sxs-lookup"><span data-stu-id="4fa28-133">Azure subscriptions and hello individual Azure services like Batch all have default quotas that limit hello number of certain entities within them.</span></span> <span data-ttu-id="4fa28-134">As cotas do saudação padrão para as assinaturas do Azure, consulte [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="4fa28-134">For hello default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="4fa28-135">As cotas do hello padrão do serviço de lote de hello, consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="4fa28-135">For hello default quotas of hello Batch service, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="4fa28-136">Usando a biblioteca do hello Batch Management .NET, você pode verificar essas cotas em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4fa28-136">By using hello Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="4fa28-137">Isso permite que você toomake decisões de alocação antes de adicionar contas ou recursos, como pools de computação e nós de computação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-137">This enables you toomake allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="4fa28-138">Verificar uma assinatura do Azure para cotas de conta do Lote</span><span class="sxs-lookup"><span data-stu-id="4fa28-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="4fa28-139">Antes de criar uma conta de lote em uma região, você pode verificar sua assinatura do Azure toosee se você é capaz de tooadd uma conta nessa região.</span><span class="sxs-lookup"><span data-stu-id="4fa28-139">Before creating a Batch account in a region, you can check your Azure subscription toosee whether you are able tooadd an account in that region.</span></span>

<span data-ttu-id="4fa28-140">No trecho de código Olá abaixo, podemos usar primeiro [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget uma coleção de todas as contas de lote que estão dentro de uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="4fa28-140">In hello code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] tooget a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="4fa28-141">Depois que obtivemos essa coleção, podemos determinar quantas contas estão na região de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-141">Once we've obtained this collection, we determine how many accounts are in hello target region.</span></span> <span data-ttu-id="4fa28-142">Em seguida, usamos [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain Olá cota da conta em lotes e determinar o número de contas (se houver) pode ser criado nessa região.</span><span class="sxs-lookup"><span data-stu-id="4fa28-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] tooobtain hello Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="4fa28-143">No trecho de saudação acima, `creds` é uma instância de [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="4fa28-143">In hello snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="4fa28-144">toosee um exemplo de como criar esse objeto, consulte Olá [AccountManagement] [ acct_mgmt_sample] exemplo de código no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4fa28-144">toosee an example of creating this object, see hello [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="4fa28-145">Verificar as cotas de recursos de computação na conta do Lote</span><span class="sxs-lookup"><span data-stu-id="4fa28-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="4fa28-146">Antes de aumentar os recursos de computação em sua solução de lote, você pode verificar recursos do hello tooensure deseja tooallocate não exceder as cotas da conta hello.</span><span class="sxs-lookup"><span data-stu-id="4fa28-146">Before increasing compute resources in your Batch solution, you can check tooensure hello resources you want tooallocate won't exceed hello account's quotas.</span></span> <span data-ttu-id="4fa28-147">No trecho de código Olá abaixo, imprimir informações de cota de saudação para Olá conta em lotes chamada `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="4fa28-147">In hello code snippet below, we print hello quota information for hello Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="4fa28-148">Em seu próprio aplicativo, você pode usar toodetermine essas informações se conta Olá pode manipular Olá recursos adicionais toobe criado.</span><span class="sxs-lookup"><span data-stu-id="4fa28-148">In your own application, you could use such information toodetermine whether hello account can handle hello additional resources toobe created.</span></span>

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="4fa28-149">Existem cotas padrão para serviços e assinaturas do Azure, muitos desses limites podem ser gerados emitindo uma solicitação no hello [portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="4fa28-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="4fa28-150">Por exemplo, consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md) para obter instruções sobre como aumentar cotas de conta de lote.</span><span class="sxs-lookup"><span data-stu-id="4fa28-150">For example, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="4fa28-151">Usar o Azure AD com o .NET de Gerenciamento de Lote</span><span class="sxs-lookup"><span data-stu-id="4fa28-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="4fa28-152">biblioteca do Hello Batch Management .NET é um cliente do provedor de recursos do Azure e é usada junto com [do Azure Resource Manager] [ resman_overview] toomanage conta recursos de forma programática.</span><span class="sxs-lookup"><span data-stu-id="4fa28-152">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage account resources programmatically.</span></span> <span data-ttu-id="4fa28-153">AD do Azure é necessário tooauthenticate solicitações feitas por meio de qualquer cliente de provedor de recursos do Azure, incluindo a biblioteca de Batch Management .NET Olá e [do Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="4fa28-153">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="4fa28-154">Para obter informações sobre como usar o AD do Azure com biblioteca de Batch Management .NET hello, consulte [soluções de lote do uso do Azure Active Directory tooauthenticate](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="4fa28-154">For information about using Azure AD with hello Batch Management .NET library, see [Use Azure Active Directory tooauthenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="4fa28-155">Projeto de exemplo no GitHub</span><span class="sxs-lookup"><span data-stu-id="4fa28-155">Sample project on GitHub</span></span>

<span data-ttu-id="4fa28-156">toosee Batch Management .NET em ação, confira Olá [AccountManagment] [ acct_mgmt_sample] projeto de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4fa28-156">toosee Batch Management .NET in action, check out hello [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="4fa28-157">Olá AccountManagment aplicativo de exemplo demonstra Olá seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="4fa28-157">hello AccountManagment sample application demonstrates hello following operations:</span></span>

1. <span data-ttu-id="4fa28-158">Adquira um token de segurança no Azure AD usando a [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="4fa28-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="4fa28-159">Se o usuário Olá não tiver entrado, será solicitado que as credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa28-159">If hello user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="4fa28-160">Com o token de segurança Olá obtido do AD do Azure, crie um [SubscriptionClient] [ resman_subclient] tooquery do Azure para obter uma lista de assinaturas associadas à conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-160">With hello security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] tooquery Azure for a list of subscriptions associated with hello account.</span></span> <span data-ttu-id="4fa28-161">Olá usuário pode selecionar uma assinatura lista Olá se ele contém mais de uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="4fa28-161">hello user can select a subscription from hello list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="4fa28-162">Obtenha as credenciais associadas à assinatura de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="4fa28-162">Get credentials associated with hello selected subscription.</span></span>
4. <span data-ttu-id="4fa28-163">Criar um [ResourceManagementClient] [ resman_client] objeto usando credenciais de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-163">Create a [ResourceManagementClient][resman_client] object by using hello credentials.</span></span>
5. <span data-ttu-id="4fa28-164">Use um [ResourceManagementClient] [ resman_client] toocreate um grupo de recursos do objeto.</span><span class="sxs-lookup"><span data-stu-id="4fa28-164">Use a [ResourceManagementClient][resman_client] object toocreate a resource group.</span></span>
6. <span data-ttu-id="4fa28-165">Use um [BatchManagementClient] [ net_mgmt_client] objeto tooperform várias operações de conta de lote:</span><span class="sxs-lookup"><span data-stu-id="4fa28-165">Use a [BatchManagementClient][net_mgmt_client] object tooperform several Batch account operations:</span></span>
   * <span data-ttu-id="4fa28-166">Crie uma conta de lote no novo grupo de recursos hello.</span><span class="sxs-lookup"><span data-stu-id="4fa28-166">Create a Batch account in hello new resource group.</span></span>
   * <span data-ttu-id="4fa28-167">Obter Olá recentemente criado a conta de serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-167">Get hello newly created account from hello Batch service.</span></span>
   * <span data-ttu-id="4fa28-168">Chaves da conta para a nova conta de saudação Olá impressão.</span><span class="sxs-lookup"><span data-stu-id="4fa28-168">Print hello account keys for hello new account.</span></span>
   * <span data-ttu-id="4fa28-169">Regenerar uma nova chave primária para a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-169">Regenerate a new primary key for hello account.</span></span>
   * <span data-ttu-id="4fa28-170">Imprima informações de cota de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-170">Print hello quota information for hello account.</span></span>
   * <span data-ttu-id="4fa28-171">Imprima informações de cota de saudação para assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-171">Print hello quota information for hello subscription.</span></span>
   * <span data-ttu-id="4fa28-172">Imprima todas as contas de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-172">Print all accounts within hello subscription.</span></span>
   * <span data-ttu-id="4fa28-173">Exclua a conta recém-criada.</span><span class="sxs-lookup"><span data-stu-id="4fa28-173">Delete newly created account.</span></span>
7. <span data-ttu-id="4fa28-174">Exclua grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fa28-174">Delete hello resource group.</span></span>

<span data-ttu-id="4fa28-175">Antes de excluir o grupo de contas e recursos de lote de saudação recentemente criado, você pode exibi-los no hello [portal do Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="4fa28-175">Before deleting hello newly created Batch account and resource group, you can view them in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="4fa28-176">aplicativo de exemplo hello toorun com êxito, você deve primeiro registrá-lo com seu locatário do AD do Azure em hello Azure portal e conceda permissões toohello API do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa28-176">toorun hello sample application successfully, you must first register it with your Azure AD tenant in hello Azure portal and grant permissions toohello Azure Resource Manager API.</span></span> <span data-ttu-id="4fa28-177">Execute as etapas de saudação fornecidas no [soluções de gerenciamento de lote de autenticar com o Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="4fa28-177">Follow hello steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "O que é o Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Cenários de autenticação do Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrando aplicativos com o Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
