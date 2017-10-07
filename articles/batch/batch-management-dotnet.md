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
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a>Gerenciar contas de lote e cotas com biblioteca de cliente de gerenciamento em lote Olá para .NET

> [!div class="op_single_selector"]
> * [Portal do Azure](batch-account-create-portal.md)
> * [.NET de Gerenciamento do Lote](batch-management-dotnet.md)
> 
> 

Você pode diminuir manutenção sobrecarga em seus aplicativos de lote do Azure usando Olá [Batch Management .NET] [ api_mgmt_net] criação de conta do lote de tooautomate de biblioteca, exclusão, gerenciamento de chaves e descoberta de cota.

* **Criar e excluir contas do Lote** em qualquer região. Se, por exemplo, como um fornecedor de software independente (ISV) fornece um serviço para clientes em que cada um é atribuída a uma conta de lote separada para fins de cobrança, você pode adicionar conta criação e exclusão recursos tooyour portal do cliente.
* **Recuperar e regenerar chaves de conta** programaticamente para qualquer uma de suas contas do Lote. Isso pode ajudá-lo a atender às políticas de segurança que impõem substituição periódica ou expiração de chaves de conta. Quando você tiver várias contas do Lote em várias regiões do Azure, a automação desse processo de substituição aumentará a eficiência da solução.
* **Verifique as cotas de conta** e tomar Olá tentativa e erro suposições determinando quais contas de lote tem que limites. Ao verificar suas cotas de conta antes de iniciar trabalhos, de criar pools ou de adicionar nós de computação, você poderá ajustar proativamente quando ou onde esses recursos de computação serão criados. Você pode determinar quais contas exigem aumento de cota antes da alocação de recursos adicionais a elas.
* **Combine recursos de outros serviços do Azure** para uma experiência de gerenciamento completo – usando o Batch Management .NET, [Active Directory do Azure][aad_about]e hello [Azure Gerenciador de recursos de] [ resman_overview] juntos em Olá mesmo aplicativo. Usando esses recursos e suas APIs, fornecer uma experiência de autenticação ininterrupto, Olá toocreate de capacidade e excluir grupos de recursos e capacidades de saudação descritos acima para uma solução de gerenciamento de ponta a ponta.

> [!NOTE]
> Enquanto este artigo enfoca o gerenciamento programático de saudação de suas contas, chaves e cotas do lote, você pode executar muitas dessas atividades usando Olá [portal do Azure][azure_portal]. Para obter mais informações, consulte [criar uma conta de lote do Azure usando o portal do Azure de saudação](batch-account-create-portal.md) e [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a>Criar e excluir contas do Lote
Conforme mencionado, um dos principais recursos de saudação do hello API de gerenciamento do lote é toocreate e excluir contas de lote em uma região do Azure. Assim, use toodo [BatchManagementClient.Account.CreateAsync] [ net_create] e [DeleteAsync][net_delete], ou suas contrapartes síncronas.

Hello trecho de código a seguir cria uma conta, obtém Olá recentemente criado a conta de serviço de lote de saudação e, em seguida, exclui-lo. Neste trecho e Olá outros neste artigo, `batchManagementClient` é uma instância completamente inicializada de [BatchManagementClient][net_mgmt_client].

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
> Aplicativos que usam a biblioteca de Batch Management .NET hello e sua classe BatchManagementClient precisam **administrador de serviço** ou **coadministrator** acessar toohello assinatura que possui Olá Conta de lote toobe gerenciado. Para obter mais informações, consulte Olá [Active Directory do Azure](#azure-active-directory) seção e hello [AccountManagement] [ acct_mgmt_sample] exemplo de código.
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>Recuperar e regenerar chaves de conta
Obtenha as chaves da conta principal e secundária de qualquer conta do Lote em sua assinatura usando [ListKeysAsync][net_list_keys]. É possível regenerar essas chaves usando [RegenerateKeyAsync][net_regenerate_keys].

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
> Você pode criar um fluxo de trabalho simplificado de conexão para os aplicativos de gerenciamento. Primeiro, obtenha uma chave de conta para conta do lote Olá desejar toomanage com [ListKeysAsync][net_list_keys]. Em seguida, usar essa chave durante a inicialização da biblioteca do .NET em lotes Olá [BatchSharedKeyCredentials] [ net_sharedkeycred] classe, que é usado ao inicializar [BatchClient] [net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>Verificar a assinatura e cotas da conta do Lote do Azure
As assinaturas do Azure e Olá serviços individuais do Azure como lote todos têm cotas padrão que limitam o número de saudação de determinadas entidades dentro deles. As cotas do saudação padrão para as assinaturas do Azure, consulte [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md). As cotas do hello padrão do serviço de lote de hello, consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md). Usando a biblioteca do hello Batch Management .NET, você pode verificar essas cotas em seus aplicativos. Isso permite que você toomake decisões de alocação antes de adicionar contas ou recursos, como pools de computação e nós de computação.

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>Verificar uma assinatura do Azure para cotas de conta do Lote
Antes de criar uma conta de lote em uma região, você pode verificar sua assinatura do Azure toosee se você é capaz de tooadd uma conta nessa região.

No trecho de código Olá abaixo, podemos usar primeiro [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget uma coleção de todas as contas de lote que estão dentro de uma assinatura. Depois que obtivemos essa coleção, podemos determinar quantas contas estão na região de destino de saudação. Em seguida, usamos [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain Olá cota da conta em lotes e determinar o número de contas (se houver) pode ser criado nessa região.

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

No trecho de saudação acima, `creds` é uma instância de [TokenCloudCredentials][azure_tokencreds]. toosee um exemplo de como criar esse objeto, consulte Olá [AccountManagement] [ acct_mgmt_sample] exemplo de código no GitHub.

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>Verificar as cotas de recursos de computação na conta do Lote
Antes de aumentar os recursos de computação em sua solução de lote, você pode verificar recursos do hello tooensure deseja tooallocate não exceder as cotas da conta hello. No trecho de código Olá abaixo, imprimir informações de cota de saudação para Olá conta em lotes chamada `mybatchaccount`. Em seu próprio aplicativo, você pode usar toodetermine essas informações se conta Olá pode manipular Olá recursos adicionais toobe criado.

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
> Existem cotas padrão para serviços e assinaturas do Azure, muitos desses limites podem ser gerados emitindo uma solicitação no hello [portal do Azure][azure_portal]. Por exemplo, consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md) para obter instruções sobre como aumentar cotas de conta de lote.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>Usar o Azure AD com o .NET de Gerenciamento de Lote

biblioteca do Hello Batch Management .NET é um cliente do provedor de recursos do Azure e é usada junto com [do Azure Resource Manager] [ resman_overview] toomanage conta recursos de forma programática. AD do Azure é necessário tooauthenticate solicitações feitas por meio de qualquer cliente de provedor de recursos do Azure, incluindo a biblioteca de Batch Management .NET Olá e [do Azure Resource Manager][resman_overview]. Para obter informações sobre como usar o AD do Azure com biblioteca de Batch Management .NET hello, consulte [soluções de lote do uso do Azure Active Directory tooauthenticate](batch-aad-auth.md). 

## <a name="sample-project-on-github"></a>Projeto de exemplo no GitHub

toosee Batch Management .NET em ação, confira Olá [AccountManagment] [ acct_mgmt_sample] projeto de exemplo no GitHub. Olá AccountManagment aplicativo de exemplo demonstra Olá seguintes operações:

1. Adquira um token de segurança no Azure AD usando a [ADAL][aad_adal]. Se o usuário Olá não tiver entrado, será solicitado que as credenciais do Azure.
2. Com o token de segurança Olá obtido do AD do Azure, crie um [SubscriptionClient] [ resman_subclient] tooquery do Azure para obter uma lista de assinaturas associadas à conta de saudação. Olá usuário pode selecionar uma assinatura lista Olá se ele contém mais de uma assinatura.
3. Obtenha as credenciais associadas à assinatura de saudação selecionada.
4. Criar um [ResourceManagementClient] [ resman_client] objeto usando credenciais de saudação.
5. Use um [ResourceManagementClient] [ resman_client] toocreate um grupo de recursos do objeto.
6. Use um [BatchManagementClient] [ net_mgmt_client] objeto tooperform várias operações de conta de lote:
   * Crie uma conta de lote no novo grupo de recursos hello.
   * Obter Olá recentemente criado a conta de serviço de lote de saudação.
   * Chaves da conta para a nova conta de saudação Olá impressão.
   * Regenerar uma nova chave primária para a conta de saudação.
   * Imprima informações de cota de saudação para conta de saudação.
   * Imprima informações de cota de saudação para assinatura de saudação.
   * Imprima todas as contas de assinatura de saudação.
   * Exclua a conta recém-criada.
7. Exclua grupo de recursos de saudação.

Antes de excluir o grupo de contas e recursos de lote de saudação recentemente criado, você pode exibi-los no hello [portal do Azure][azure_portal]:

aplicativo de exemplo hello toorun com êxito, você deve primeiro registrá-lo com seu locatário do AD do Azure em hello Azure portal e conceda permissões toohello API do Gerenciador de recursos do Azure. Execute as etapas de saudação fornecidas no [soluções de gerenciamento de lote de autenticar com o Active Directory](batch-aad-auth-management.md).


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
