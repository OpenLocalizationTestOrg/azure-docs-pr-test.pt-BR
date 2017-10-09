---
ms.assetid: 
title: aaaAzure chave de Cofre de chaves da conta de armazenamento
description: "Chaves da conta de armazenamento fornecem uma integração obterá entre o Azure Key Vault e chave de acesso baseado em tooAzure conta de armazenamento."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="02b5e-103">Chaves de conta de Armazenamento do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="02b5e-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="02b5e-104">Antes de chaves de conta do armazenamento de Cofre de chave do Azure, os desenvolvedores tinham toomanage suas próprias chaves de conta de armazenamento do Azure (ASA) e girar manualmente ou por meio de um objeto de automação externo.</span><span class="sxs-lookup"><span data-stu-id="02b5e-104">Before Azure Key Vault Storage Account Keys, developers had toomanage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="02b5e-105">Agora, as Chave de Conta de Armazenamento do Key Vault são implementadas como [Segredos do Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) para autenticação com uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="02b5e-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="02b5e-106">recurso principal do Hello ASA gerencia rotação segreda para você e elimina a necessidade de saudação de seu contato direto com uma chave ASA oferecendo assinaturas de acesso compartilhado (SAS) como um método.</span><span class="sxs-lookup"><span data-stu-id="02b5e-106">hello ASA key feature manages secret rotation for you and removes hello need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="02b5e-107">Para obter mais informações gerais sobre Contas de Armazenamento do Azure, consulte [Sobre contas de armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="02b5e-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="02b5e-108">Interfaces de suporte</span><span class="sxs-lookup"><span data-stu-id="02b5e-108">Supporting interfaces</span></span>

<span data-ttu-id="02b5e-109">Olá recurso de chaves de conta de armazenamento do Azure é inicialmente disponível por meio de saudação REST, .NET / interfaces do c# e do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02b5e-109">hello Azure Storage Account keys feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="02b5e-110">Para obter mais informações, consulte [Referência do Key Vault](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="02b5e-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="02b5e-111">Comportamento de chaves da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="02b5e-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="02b5e-112">O que o Key Vault gerencia</span><span class="sxs-lookup"><span data-stu-id="02b5e-112">What Key Vault manages</span></span>

<span data-ttu-id="02b5e-113">O Key Vault executa várias funções de gerenciamento interno em seu nome quando você usa Chaves de Conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="02b5e-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="02b5e-114">O Azure Key Vault gerencia chaves de uma ASA (Conta de Armazenamento do Azure).</span><span class="sxs-lookup"><span data-stu-id="02b5e-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="02b5e-115">Internamente, o Azure Key Vault pode listar (sincronizar) chaves com uma Conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="02b5e-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="02b5e-116">Gera novamente o Cofre de chaves do Azure (gira) Olá chaves periodicamente.</span><span class="sxs-lookup"><span data-stu-id="02b5e-116">Azure Key Vault regenerates (rotates) hello keys periodically.</span></span> 
    - <span data-ttu-id="02b5e-117">Valores de chave nunca são retornados na resposta toocaller.</span><span class="sxs-lookup"><span data-stu-id="02b5e-117">Key values are never returned in response toocaller.</span></span> 
    - <span data-ttu-id="02b5e-118">O Azure Key Vault gerencia chaves tanto de Contas de Armazenamento quanto de Contas de Armazenamento Clássicas.</span><span class="sxs-lookup"><span data-stu-id="02b5e-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="02b5e-119">Cofre de chaves do Azure permite que você, Olá cofre/objeto proprietário, toocreate definições de SAS (conta ou serviço SAS).</span><span class="sxs-lookup"><span data-stu-id="02b5e-119">Azure Key Vault allows you, hello vault/object owner, toocreate SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="02b5e-120">Olá valor SAS, criado usando a definição de SAS, é retornado como um segredo por meio do caminho do URI de REST de saudação.</span><span class="sxs-lookup"><span data-stu-id="02b5e-120">hello SAS value, created using SAS definition, is returned as a secret via hello REST URI path.</span></span> <span data-ttu-id="02b5e-121">Para obter mais informações, consulte [Operações de conta de armazenamento do Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="02b5e-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="02b5e-122">Diretrizes de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="02b5e-122">Naming guidance</span></span>

<span data-ttu-id="02b5e-123">Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="02b5e-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="02b5e-124">Um nome de definição de SAS deve ter de 1 a 102 caracteres, contendo somente 0–9, a–z, A–Z.</span><span class="sxs-lookup"><span data-stu-id="02b5e-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="02b5e-125">Experiência do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="02b5e-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="02b5e-126">Antes das chaves de armazenamento do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="02b5e-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="02b5e-127">Os desenvolvedores usavam tooneed toodo Olá seguir práticas recomendadas com uma conta tooget chave acesso tooAzure de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="02b5e-127">Developers used tooneed toodo hello following practices with a storage account key tooget access tooAzure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="02b5e-128">Depois das chaves de armazenamento do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="02b5e-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="02b5e-129">Melhores práticas do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="02b5e-129">Developer best practices</span></span> 

- <span data-ttu-id="02b5e-130">Permita somente a suas chaves ASA toomanage de Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="02b5e-130">Only allow Key Vault toomanage your ASA keys.</span></span> <span data-ttu-id="02b5e-131">Não tente toomanage-los por conta própria, você irá interferir com processos do cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="02b5e-131">Do not attempt toomanage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="02b5e-132">Não permita ASA chaves toobe gerenciado por mais de um objeto de Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="02b5e-132">Do not allow ASA keys toobe managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="02b5e-133">Se você precisar toomanually regenerar suas chaves ASA, recomendamos que você regenerá-los por meio do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="02b5e-133">If you need toomanually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="02b5e-134">Introdução</span><span class="sxs-lookup"><span data-stu-id="02b5e-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="02b5e-135">Configuração para permissões de RBAC (controle de acesso baseadas em função)</span><span class="sxs-lookup"><span data-stu-id="02b5e-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="02b5e-136">Cofre de chaves precisa de permissões muito*lista* e *regenerar* chaves para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="02b5e-136">Key Vault needs permissions too*list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="02b5e-137">Configure permissões utilizando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="02b5e-137">Set up these permissions using hello following steps:</span></span>

- <span data-ttu-id="02b5e-138">Obter ObjectId do Key Vault:</span><span class="sxs-lookup"><span data-stu-id="02b5e-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="02b5e-139">Atribua função de operador de chave de armazenamento tooAzure identidade de Cofre de chave:</span><span class="sxs-lookup"><span data-stu-id="02b5e-139">Assign Storage Key Operator role tooAzure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="02b5e-140">Para um tipo de conta clássico, defina o parâmetro de função de saudação muito*"Clássico armazenamento chave operador serviço de função de conta"*.</span><span class="sxs-lookup"><span data-stu-id="02b5e-140">For a classic account type, set hello role parameter too*"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="02b5e-141">Integração da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="02b5e-141">Storage account onboarding</span></span> 

<span data-ttu-id="02b5e-142">Exemplo: Como um proprietário de objeto de Cofre de chaves que você adicionar um armazenamento de conta objeto tooyour Azure Key Vault tooonboard uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="02b5e-142">Example: As a Key Vault object owner you add a storage account object tooyour Azure Key Vault tooonboard a storage account.</span></span>

<span data-ttu-id="02b5e-143">Durante a integração, o Cofre de chaves precisa tooverify se identidade Olá da conta de integração Olá também tem permissões*lista* e muito*regenerar* chaves de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="02b5e-143">During onboarding, Key Vault needs tooverify that hello identity of hello onboarding account has permissions too*list* and too*regenerate* storage keys.</span></span> <span data-ttu-id="02b5e-144">Em ordem tooverify essas permissões, o Cofre de chaves obtém um OBO (em nome de) token do serviço de autenticação hello, público definido tooAzure Gerenciador de recursos e torna um *lista* serviço de armazenamento do Azure toohello chamada de chave.</span><span class="sxs-lookup"><span data-stu-id="02b5e-144">In order tooverify these permissions, Key Vault gets an OBO (On Behalf Of) token from hello authentication service, audience set tooAzure Resource Manager, and makes a *list* key call toohello Azure Storage service.</span></span> <span data-ttu-id="02b5e-145">Se hello *lista* chamada falhar, Olá Falha na criação do objeto com um código de status do HTTP para o Cofre de chaves *proibido*.</span><span class="sxs-lookup"><span data-stu-id="02b5e-145">If hello *list* call fails, hello Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="02b5e-146">chaves de saudação listadas dessa maneira são armazenados em cache com o armazenamento de entidade do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="02b5e-146">hello keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="02b5e-147">Cofre de chaves deve verificar se tem identidade Olá *regenerar* permissões antes que ele pode apropriar-se de regenerar as chaves.</span><span class="sxs-lookup"><span data-stu-id="02b5e-147">Key Vault must verify that hello identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="02b5e-148">tooverify que Olá identidade, via token OBO, bem como Olá identidade de terceiros primeiro cofre de chaves com essas permissões:</span><span class="sxs-lookup"><span data-stu-id="02b5e-148">tooverify that hello identity, via OBO token, as well as hello Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="02b5e-149">Cofre de chaves lista permissões de RBAC no recurso de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="02b5e-149">Key Vault lists RBAC permissions on hello storage account resource.</span></span>
- <span data-ttu-id="02b5e-150">Cofre de chaves valida resposta Olá por meio de ações e ações de não correspondência da expressão regular.</span><span class="sxs-lookup"><span data-stu-id="02b5e-150">Key Vault validates hello response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="02b5e-151">Encontre alguns exemplos de suporte em [Key Vault – Amostras de Chaves de Conta de Armazenamento Gerenciado](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span><span class="sxs-lookup"><span data-stu-id="02b5e-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="02b5e-152">Se não tiver a identidade de saudação *regenerar* permissões ou se a primeira identidade de terceiros do cofre da chave não tiver *lista* ou *regenerar* permissão, em seguida, Olá integração Falha na solicitação retornando um código de erro apropriado e uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="02b5e-152">If hello identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then hello onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="02b5e-153">token OBO Olá só funcionará quando você usa o primário, os aplicativos cliente nativos do PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="02b5e-153">hello OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="02b5e-154">Outros aplicativos</span><span class="sxs-lookup"><span data-stu-id="02b5e-154">Other applications</span></span>

- <span data-ttu-id="02b5e-155">Tokens SAS, construídas usando chaves de conta de armazenamento de Cofre de chaves, fornecem mais acesso controlado tooan conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="02b5e-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access tooan Azure storage account.</span></span> <span data-ttu-id="02b5e-156">Para obter mais informações, confira [Como usar assinaturas de acesso compartilhado](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="02b5e-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="02b5e-157">Consulte também</span><span class="sxs-lookup"><span data-stu-id="02b5e-157">See also</span></span>

- [<span data-ttu-id="02b5e-158">Sobre chaves, segredos e certificados</span><span class="sxs-lookup"><span data-stu-id="02b5e-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="02b5e-159">Blog da equipe do Key Vault</span><span class="sxs-lookup"><span data-stu-id="02b5e-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
