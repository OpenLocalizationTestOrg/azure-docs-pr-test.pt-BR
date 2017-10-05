---
ms.assetid: 
title: Chaves de conta de Armazenamento do Azure Key Vault
description: "Chaves da conta de armazenamento fornecem uma integração contínua entre o Azure Key Vault e o acesso baseado em chave para a Conta de Armazenamento do Azure."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: 3148088c88236c64e089fd25c98eb8ac7cdcbfea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="9a69a-103">Chaves de conta de Armazenamento do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9a69a-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="9a69a-104">Antes das Chaves de Conta de Armazenamento do Azure Key Vault, os desenvolvedores precisavam gerenciar suas próprias chaves de ASA (Conta de Armazenamento do Azure) e girá-las manualmente ou por meio de um automação externa.</span><span class="sxs-lookup"><span data-stu-id="9a69a-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="9a69a-105">Agora, as Chave de Conta de Armazenamento do Key Vault são implementadas como [Segredos do Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) para autenticação com uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a69a-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="9a69a-106">O recurso de chave ASA gerencia a rotação secreta para você e elimina a necessidade de contato direto com uma chave ASA ao oferecer SAS (Assinaturas de Acesso Compartilhado) como um método.</span><span class="sxs-lookup"><span data-stu-id="9a69a-106">The ASA key feature manages secret rotation for you and removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="9a69a-107">Para obter mais informações gerais sobre Contas de Armazenamento do Azure, consulte [Sobre contas de armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9a69a-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="9a69a-108">Interfaces de suporte</span><span class="sxs-lookup"><span data-stu-id="9a69a-108">Supporting interfaces</span></span>

<span data-ttu-id="9a69a-109">O recurso de chaves da Conta de Armazenamento do Azure está inicialmente disponível por meio das interfaces REST, .NET/C# e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a69a-109">The Azure Storage Account keys feature is initially available through the REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="9a69a-110">Para obter mais informações, consulte [Referência do Key Vault](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="9a69a-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="9a69a-111">Comportamento de chaves da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="9a69a-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="9a69a-112">O que o Key Vault gerencia</span><span class="sxs-lookup"><span data-stu-id="9a69a-112">What Key Vault manages</span></span>

<span data-ttu-id="9a69a-113">O Key Vault executa várias funções de gerenciamento interno em seu nome quando você usa Chaves de Conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9a69a-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="9a69a-114">O Azure Key Vault gerencia chaves de uma ASA (Conta de Armazenamento do Azure).</span><span class="sxs-lookup"><span data-stu-id="9a69a-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="9a69a-115">Internamente, o Azure Key Vault pode listar (sincronizar) chaves com uma Conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a69a-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="9a69a-116">O Azure Key Vault gera novamente (gira) as chaves periodicamente.</span><span class="sxs-lookup"><span data-stu-id="9a69a-116">Azure Key Vault regenerates (rotates) the keys periodically.</span></span> 
    - <span data-ttu-id="9a69a-117">Os valores de chave nunca são retornados em resposta ao chamador.</span><span class="sxs-lookup"><span data-stu-id="9a69a-117">Key values are never returned in response to caller.</span></span> 
    - <span data-ttu-id="9a69a-118">O Azure Key Vault gerencia chaves tanto de Contas de Armazenamento quanto de Contas de Armazenamento Clássicas.</span><span class="sxs-lookup"><span data-stu-id="9a69a-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="9a69a-119">O Azure Key Vault permite que você, o proprietário do cofre/objeto, crie definições de SAS (SAS de conta ou serviço).</span><span class="sxs-lookup"><span data-stu-id="9a69a-119">Azure Key Vault allows you, the vault/object owner, to create SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="9a69a-120">O valor SAS, criado usando a definição de SAS, é retornado como um segredo por meio do caminho do URI REST.</span><span class="sxs-lookup"><span data-stu-id="9a69a-120">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span></span> <span data-ttu-id="9a69a-121">Para obter mais informações, consulte [Operações de conta de armazenamento do Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="9a69a-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="9a69a-122">Diretrizes de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="9a69a-122">Naming guidance</span></span>

<span data-ttu-id="9a69a-123">Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9a69a-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="9a69a-124">Um nome de definição de SAS deve ter de 1 a 102 caracteres, contendo somente 0–9, a–z, A–Z.</span><span class="sxs-lookup"><span data-stu-id="9a69a-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="9a69a-125">Experiência do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="9a69a-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="9a69a-126">Antes das chaves de armazenamento do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9a69a-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="9a69a-127">Os desenvolvedores costumavam precisar fazer o seguinte com uma chave de conta de armazenamento para obterem acesso ao armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a69a-127">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="9a69a-128">Depois das chaves de armazenamento do Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9a69a-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure to set storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command to get Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using the SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and the Blob storage endpoint to create a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about to expire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="9a69a-129">Melhores práticas do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="9a69a-129">Developer best practices</span></span> 

- <span data-ttu-id="9a69a-130">Permita somente que o Key Vault gerencie suas chaves ASA.</span><span class="sxs-lookup"><span data-stu-id="9a69a-130">Only allow Key Vault to manage your ASA keys.</span></span> <span data-ttu-id="9a69a-131">Não tentar gerenciá-las você mesmo, você interferirá nos processos do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9a69a-131">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="9a69a-132">Não permita que chaves ASA sejam gerenciadas por mais de um objeto do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9a69a-132">Do not allow ASA keys to be managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="9a69a-133">Se precisar regenerar manualmente as chaves ASA, recomendamos que você as regenere por meio do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9a69a-133">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="9a69a-134">Introdução</span><span class="sxs-lookup"><span data-stu-id="9a69a-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="9a69a-135">Configuração para permissões de RBAC (controle de acesso baseadas em função)</span><span class="sxs-lookup"><span data-stu-id="9a69a-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="9a69a-136">O Key Vault precisa de permissões para *listar* e *regenerar* chaves para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9a69a-136">Key Vault needs permissions to *list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="9a69a-137">Configure essas permissões usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9a69a-137">Set up these permissions using the following steps:</span></span>

- <span data-ttu-id="9a69a-138">Obter ObjectId do Key Vault:</span><span class="sxs-lookup"><span data-stu-id="9a69a-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="9a69a-139">Atribua a função de Operador de Chave de Armazenamento à Identidade do Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="9a69a-139">Assign Storage Key Operator role to Azure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="9a69a-140">Para um tipo de conta clássico, defina o parâmetro de função como *"Função de Serviço do Operador de Chave de Conta de Armazenamento Clássica"*.</span><span class="sxs-lookup"><span data-stu-id="9a69a-140">For a classic account type, set the role parameter to *"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="9a69a-141">Integração da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="9a69a-141">Storage account onboarding</span></span> 

<span data-ttu-id="9a69a-142">Exemplo: como um proprietário de objeto do Key Vault, você adiciona um objeto de conta de armazenamento ao seu Azure Key Vault para integrar uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9a69a-142">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span></span>

<span data-ttu-id="9a69a-143">Durante a integração, o Key Vault precisa verificar se a identidade da conta de integração tem permissões para *listar* e *regenerar* chaves de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9a69a-143">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span></span> <span data-ttu-id="9a69a-144">Para verificar essas permissões, o Key Vault obtém um token OBO (em nome de) do serviço de autenticação com público definido para o Azure Resource Manager e faz uma chamada de chave de *lista* para o serviço de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a69a-144">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span></span> <span data-ttu-id="9a69a-145">Se a chamada de *lista* falhar, a criação do objeto Key Vault falhará com o código de status HTTP *Forbidden*.</span><span class="sxs-lookup"><span data-stu-id="9a69a-145">If the *list* call fails, the Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="9a69a-146">As chaves listadas dessa maneira são armazenadas em cache com o seu armazenamento de entidade do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="9a69a-146">The keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="9a69a-147">O Key Vault deve verificar se a identidade tem permissões para *regenerar* antes de poder assumir a propriedade da regeneração das suas chaves.</span><span class="sxs-lookup"><span data-stu-id="9a69a-147">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="9a69a-148">Para verificar se a identidade, via token OBO, bem como a identidade de primeira parte do Key Vault têm essas permissões:</span><span class="sxs-lookup"><span data-stu-id="9a69a-148">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="9a69a-149">O Key Vault lista permissões de RBAC no recurso de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9a69a-149">Key Vault lists RBAC permissions on the storage account resource.</span></span>
- <span data-ttu-id="9a69a-150">O Key Vault valida a resposta por meio correspondência de expressão regular de ações e não ações.</span><span class="sxs-lookup"><span data-stu-id="9a69a-150">Key Vault validates the response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="9a69a-151">Encontre alguns exemplos de suporte em [Key Vault – Amostras de Chaves de Conta de Armazenamento Gerenciado](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span><span class="sxs-lookup"><span data-stu-id="9a69a-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="9a69a-152">Se a identidade não tiver a permissão *regenerar* ou se a identidade da primeira parte do Key Vault não tiver a permissão *lista* ou *regenerar*, a solicitação de integração falhará, retornando um código de erro apropriado e uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="9a69a-152">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="9a69a-153">O token OBO só funcionará quando você usar os aplicativos cliente nativos de primeira parte do PowerShell ou da CLI.</span><span class="sxs-lookup"><span data-stu-id="9a69a-153">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="9a69a-154">Outros aplicativos</span><span class="sxs-lookup"><span data-stu-id="9a69a-154">Other applications</span></span>

- <span data-ttu-id="9a69a-155">Tokens SAS, construídos usando chaves de conta de armazenamento do Key Vault, fornecem acesso ainda mais controlado a uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a69a-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span></span> <span data-ttu-id="9a69a-156">Para obter mais informações, confira [Como usar assinaturas de acesso compartilhado](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="9a69a-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="9a69a-157">Consulte também</span><span class="sxs-lookup"><span data-stu-id="9a69a-157">See also</span></span>

- [<span data-ttu-id="9a69a-158">Sobre chaves, segredos e certificados</span><span class="sxs-lookup"><span data-stu-id="9a69a-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="9a69a-159">Blog da equipe do Key Vault</span><span class="sxs-lookup"><span data-stu-id="9a69a-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
