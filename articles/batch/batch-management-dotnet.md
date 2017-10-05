---
title: Gerenciar recursos da conta do Lote com a biblioteca de cliente para .NET - Azure | Microsoft Docs
description: Criar, excluir e modificar recursos de conta do Lote do Azure em seus aplicativos com a biblioteca .NET de Gerenciamento do Lote.
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
ms.openlocfilehash: eafde9258222a2ab09ade2e366f9cc595a303dec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a><span data-ttu-id="b48ad-103">Gerenciar contas e cotas do Lote com a biblioteca de clientes do Gerenciamento de Lotes para .NET</span><span class="sxs-lookup"><span data-stu-id="b48ad-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b48ad-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b48ad-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="b48ad-105">.NET de Gerenciamento do Lote</span><span class="sxs-lookup"><span data-stu-id="b48ad-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="b48ad-106">É possível diminuir a sobrecarga de manutenção em seus aplicativos do Lote do Azure usando a biblioteca do [.NET de Gerenciamento do Lote][api_mgmt_net] para automatizar a criação, a exclusão, o gerenciamento de chaves e a descoberta de cotas da conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="b48ad-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="b48ad-107">**Criar e excluir contas do Lote** em qualquer região.</span><span class="sxs-lookup"><span data-stu-id="b48ad-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="b48ad-108">Se como um ISV (fornecedor independente de software), por exemplo, você fornece um serviço para os clientes no qual cada um é atribuído a uma conta do Lote separada para fins de cobrança, pode adicionar recursos de criação e exclusão de conta no portal do cliente.</span><span class="sxs-lookup"><span data-stu-id="b48ad-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span></span>
* <span data-ttu-id="b48ad-109">**Recuperar e regenerar chaves de conta** programaticamente para qualquer uma de suas contas do Lote.</span><span class="sxs-lookup"><span data-stu-id="b48ad-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="b48ad-110">Isso pode ajudá-lo a atender às políticas de segurança que impõem substituição periódica ou expiração de chaves de conta.</span><span class="sxs-lookup"><span data-stu-id="b48ad-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="b48ad-111">Quando você tiver várias contas do Lote em várias regiões do Azure, a automação desse processo de substituição aumentará a eficiência da solução.</span><span class="sxs-lookup"><span data-stu-id="b48ad-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="b48ad-112">**Verificar cotas de conta** e eliminar as suposições de tentativa e erro na determinação dos limites de cada conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="b48ad-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="b48ad-113">Ao verificar suas cotas de conta antes de iniciar trabalhos, de criar pools ou de adicionar nós de computação, você poderá ajustar proativamente quando ou onde esses recursos de computação serão criados.</span><span class="sxs-lookup"><span data-stu-id="b48ad-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="b48ad-114">Você pode determinar quais contas exigem aumento de cota antes da alocação de recursos adicionais a elas.</span><span class="sxs-lookup"><span data-stu-id="b48ad-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="b48ad-115">**Combine os recursos de outros serviços do Azure** para ter uma experiência de gerenciamento completa, usando o .NET de Gerenciamento do Lote, o [Azure Active Directory][aad_about] e o [Azure Resource Manager][resman_overview] juntos, no mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b48ad-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span></span> <span data-ttu-id="b48ad-116">Usando esses recursos e suas APIs, você pode fornecer uma experiência de autenticação, a capacidade de criação e exclusão de grupos de recursos ininterrupta, além dos recursos descritos acima para uma solução de gerenciamento de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="b48ad-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="b48ad-117">Embora este artigo se concentre no gerenciamento programático de suas contas, chaves e cotas do Lote, você poderá executar muitas dessas atividades usando o [Portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="b48ad-117">While this article focuses on the programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using the [Azure portal][azure_portal].</span></span> <span data-ttu-id="b48ad-118">Confira [Criar uma conta do Lote do Azure no Portal do Azure](batch-account-create-portal.md) e [Cotas e limites do serviço do Lote do Azure](batch-quota-limit.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="b48ad-118">For more information, see [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md) and [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="b48ad-119">Criar e excluir contas do Lote</span><span class="sxs-lookup"><span data-stu-id="b48ad-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="b48ad-120">Como mencionado, um dos principais recursos da API de Gerenciamento do Lote é criar e excluir contas do Lote em uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="b48ad-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="b48ad-121">Para fazer isso, use [BatchManagementClient.Account.CreateAsync][net_create] e [DeleteAsync][net_delete] ou suas correspondentes síncronas.</span><span class="sxs-lookup"><span data-stu-id="b48ad-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="b48ad-122">O trecho de código a seguir cria uma conta, obtém a conta recém-criada do serviço de Lote, então, a exclui.</span><span class="sxs-lookup"><span data-stu-id="b48ad-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span></span> <span data-ttu-id="b48ad-123">Neste e em outros trechos neste artigo, `batchManagementClient` é uma instância completamente inicializada de [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="b48ad-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get the new account from the Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete the account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="b48ad-124">Os aplicativos que usam a biblioteca do .NET de Gerenciamento do Lote e sua classe BatchManagementClient exigem o acesso de **administrador de serviços** ou de **coadministrador** à assinatura que possui a conta do Lote a ser gerenciada.</span><span class="sxs-lookup"><span data-stu-id="b48ad-124">Applications that use the Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access to the subscription that owns the Batch account to be managed.</span></span> <span data-ttu-id="b48ad-125">Para obter mais informações, consulte a seção [Azure Active Directory](#azure-active-directory) abaixo e o exemplo de código [AccountManagement][acct_mgmt_sample].</span><span class="sxs-lookup"><span data-stu-id="b48ad-125">For more information, see the [Azure Active Directory](#azure-active-directory) section and the [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="b48ad-126">Recuperar e regenerar chaves de conta</span><span class="sxs-lookup"><span data-stu-id="b48ad-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="b48ad-127">Obtenha as chaves da conta principal e secundária de qualquer conta do Lote em sua assinatura usando [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="b48ad-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="b48ad-128">É possível regenerar essas chaves usando [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="b48ad-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print the primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate the primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="b48ad-129">Você pode criar um fluxo de trabalho simplificado de conexão para os aplicativos de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="b48ad-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="b48ad-130">Primeiro, obtenha uma chave de conta para a conta do Lote que você deseja gerenciar com [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="b48ad-130">First, obtain an account key for the Batch account you wish to manage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="b48ad-131">Em seguida, use essa chave ao inicializar a classe [BatchSharedKeyCredentials][net_sharedkeycred] da biblioteca .NET do Lote, que é usada ao inicializar [BatchClient][net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="b48ad-131">Then, use this key when initializing the Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="b48ad-132">Verificar a assinatura e cotas da conta do Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="b48ad-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="b48ad-133">As assinaturas do Azure e os serviços Azure individuais, como o Lote, têm cotas padrão limitando o número de determinadas entidades neles.</span><span class="sxs-lookup"><span data-stu-id="b48ad-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span></span> <span data-ttu-id="b48ad-134">Para obter as cotas padrão das assinaturas do Azure, veja [Assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b48ad-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="b48ad-135">Para obter as cotas padrão do serviço do Lote, veja [Cotas e limites para o serviço do Lote do Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="b48ad-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="b48ad-136">Usando a biblioteca .NET de Gerenciamento de Lotes, você pode verificar essas cotas em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b48ad-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="b48ad-137">Isso permite que você tome decisões de alocação antes de adicionar contas ou recursos de computação, como pools e nós de computação.</span><span class="sxs-lookup"><span data-stu-id="b48ad-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="b48ad-138">Verificar uma assinatura do Azure para cotas de conta do Lote</span><span class="sxs-lookup"><span data-stu-id="b48ad-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="b48ad-139">Antes de criar uma conta do Lote em uma região, verifique a sua assinatura do Azure para ver se é possível adicionar uma conta nessa região.</span><span class="sxs-lookup"><span data-stu-id="b48ad-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span></span>

<span data-ttu-id="b48ad-140">No trecho de código abaixo, primeiro usamos [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] para obter uma coleção de todas as contas do Lote em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="b48ad-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="b48ad-141">Depois que obtivemos essa coleção, podemos determinar quantas contas estão na região de destino.</span><span class="sxs-lookup"><span data-stu-id="b48ad-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span></span> <span data-ttu-id="b48ad-142">Em seguida, usamos [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] para obter a cota da conta do Lote e determinar quantas contas (se houver) podem ser criadas nessa região.</span><span class="sxs-lookup"><span data-stu-id="b48ad-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within the subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within the target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get the account quota for the specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in the target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in the {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="b48ad-143">No trecho acima, `creds` é uma instância de [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="b48ad-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="b48ad-144">Para ver um exemplo de como criar esse objeto, confira o exemplo de código [AccountManagement][acct_mgmt_sample] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="b48ad-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="b48ad-145">Verificar as cotas de recursos de computação na conta do Lote</span><span class="sxs-lookup"><span data-stu-id="b48ad-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="b48ad-146">Antes de aumentar os recursos de computação em sua solução do Lote, você poderá garantir que os recursos que deseja alocar não excedam as cotas da conta.</span><span class="sxs-lookup"><span data-stu-id="b48ad-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span></span> <span data-ttu-id="b48ad-147">No trecho de código abaixo, imprimimos as informações de cota para a conta do Lote chamada `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="b48ad-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="b48ad-148">Em seu próprio aplicativo, você pode usar essas informações para determinar se a conta pode lidar com os recursos adicionais a serem criados.</span><span class="sxs-lookup"><span data-stu-id="b48ad-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span></span>

```csharp
// First obtain the Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print the compute resource quotas for the account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="b48ad-149">Embora existam cotas padrão para assinaturas e serviços do Azure, muitos desses limites podem ser elevados emitindo uma solicitação no [Portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="b48ad-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in the [Azure portal][azure_portal].</span></span> <span data-ttu-id="b48ad-150">Por exemplo, veja [Cotas e limites para o serviço do Lote do Azure](batch-quota-limit.md) para obter instruções sobre como aumentar suas cotas da conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="b48ad-150">For example, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="b48ad-151">Usar o Azure AD com o .NET de Gerenciamento de Lote</span><span class="sxs-lookup"><span data-stu-id="b48ad-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="b48ad-152">A biblioteca do .NET de Gerenciamento de Lote é um cliente de provedor de recursos do Azure e é usada junto com o [Azure Resource Manager][resman_overview] para gerenciar recursos de conta de forma programática.</span><span class="sxs-lookup"><span data-stu-id="b48ad-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span></span> <span data-ttu-id="b48ad-153">O Azure AD é necessário para autenticar solicitações feitas por meio de qualquer cliente de provedor de recursos do Azure, incluindo a biblioteca do .NET de Gerenciamento de Lote e por meio do [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="b48ad-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="b48ad-154">Para obter informações sobre como usar o Azure AD com a biblioteca do .NET de Gerenciamento de Lote, consulte [Usar o Azure Active Directory para autenticar soluções em Lote](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="b48ad-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="b48ad-155">Projeto de exemplo no GitHub</span><span class="sxs-lookup"><span data-stu-id="b48ad-155">Sample project on GitHub</span></span>

<span data-ttu-id="b48ad-156">Para ver o .NET de Gerenciamento do Lote em ação, confira o projeto de exemplo [AccountManagment][acct_mgmt_sample] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="b48ad-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="b48ad-157">O aplicativo de exemplo AccountManagment demonstra as seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="b48ad-157">The AccountManagment sample application demonstrates the following operations:</span></span>

1. <span data-ttu-id="b48ad-158">Adquira um token de segurança no Azure AD usando a [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="b48ad-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="b48ad-159">Se o usuário ainda não estiver conectado, será solicitado que ele forneça suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="b48ad-159">If the user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="b48ad-160">Com o token de segurança obtido no Azure AD, crie um [SubscriptionClient][resman_subclient] para consultar o Azure e obter uma lista de assinaturas associadas à conta.</span><span class="sxs-lookup"><span data-stu-id="b48ad-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span></span> <span data-ttu-id="b48ad-161">O usuário poderá selecionar uma assinatura na lista se ela contiver mais de uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="b48ad-161">The user can select a subscription from the list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="b48ad-162">Associe as credenciais à assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="b48ad-162">Get credentials associated with the selected subscription.</span></span>
4. <span data-ttu-id="b48ad-163">Crie um objeto [ResourceManagementClient][resman_client] usando as credenciais.</span><span class="sxs-lookup"><span data-stu-id="b48ad-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span></span>
5. <span data-ttu-id="b48ad-164">Use um objeto [ResourceManagementClient][resman_client] para criar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b48ad-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span></span>
6. <span data-ttu-id="b48ad-165">Use um objeto [BatchManagementClient][net_mgmt_client] para executar várias operações de conta do Lote:</span><span class="sxs-lookup"><span data-stu-id="b48ad-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span></span>
   * <span data-ttu-id="b48ad-166">Crie uma conta do Lote no novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b48ad-166">Create a Batch account in the new resource group.</span></span>
   * <span data-ttu-id="b48ad-167">Obtenha a conta recém-criada no serviço do Lote.</span><span class="sxs-lookup"><span data-stu-id="b48ad-167">Get the newly created account from the Batch service.</span></span>
   * <span data-ttu-id="b48ad-168">Imprima as chaves de conta da nova conta.</span><span class="sxs-lookup"><span data-stu-id="b48ad-168">Print the account keys for the new account.</span></span>
   * <span data-ttu-id="b48ad-169">Regenere uma nova chave primária para a conta.</span><span class="sxs-lookup"><span data-stu-id="b48ad-169">Regenerate a new primary key for the account.</span></span>
   * <span data-ttu-id="b48ad-170">Imprima as informações de cota para a conta.</span><span class="sxs-lookup"><span data-stu-id="b48ad-170">Print the quota information for the account.</span></span>
   * <span data-ttu-id="b48ad-171">Imprima as informações de cota para a assinatura.</span><span class="sxs-lookup"><span data-stu-id="b48ad-171">Print the quota information for the subscription.</span></span>
   * <span data-ttu-id="b48ad-172">Imprima todas as contas na assinatura.</span><span class="sxs-lookup"><span data-stu-id="b48ad-172">Print all accounts within the subscription.</span></span>
   * <span data-ttu-id="b48ad-173">Exclua a conta recém-criada.</span><span class="sxs-lookup"><span data-stu-id="b48ad-173">Delete newly created account.</span></span>
7. <span data-ttu-id="b48ad-174">Exclua o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b48ad-174">Delete the resource group.</span></span>

<span data-ttu-id="b48ad-175">Antes de excluir o grupo de recursos e a conta do Lote recém-criada, é possível vê-los no [portal do Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="b48ad-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="b48ad-176">Para executar o aplicativo de exemplo com êxito, primeiro é necessário registrá-lo no locatário do Azure AD no portal do Azure e conceder permissões à API do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b48ad-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span></span> <span data-ttu-id="b48ad-177">Siga as etapas fornecidas em [Autenticar soluções de gerenciamento do lote com o Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="b48ad-177">Follow the steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


<span data-ttu-id="b48ad-178">[aad_about]: ../active-directory/active-directory-whatis.md "O que é o Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="b48ad-178">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="b48ad-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Cenários de autenticação do Azure AD"</span><span class="sxs-lookup"><span data-stu-id="b48ad-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="b48ad-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrando aplicativos com o Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="b48ad-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
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
