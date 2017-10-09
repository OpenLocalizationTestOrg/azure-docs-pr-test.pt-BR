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
# <a name="azure-key-vault-storage-account-keys"></a>Chaves de conta de Armazenamento do Azure Key Vault

Antes de chaves de conta do armazenamento de Cofre de chave do Azure, os desenvolvedores tinham toomanage suas próprias chaves de conta de armazenamento do Azure (ASA) e girar manualmente ou por meio de um objeto de automação externo. Agora, as Chave de Conta de Armazenamento do Key Vault são implementadas como [Segredos do Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) para autenticação com uma conta de Armazenamento do Azure. 

recurso principal do Hello ASA gerencia rotação segreda para você e elimina a necessidade de saudação de seu contato direto com uma chave ASA oferecendo assinaturas de acesso compartilhado (SAS) como um método. 

Para obter mais informações gerais sobre Contas de Armazenamento do Azure, consulte [Sobre contas de armazenamento do Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Interfaces de suporte

Olá recurso de chaves de conta de armazenamento do Azure é inicialmente disponível por meio de saudação REST, .NET / interfaces do c# e do PowerShell. Para obter mais informações, consulte [Referência do Key Vault](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Comportamento de chaves da conta de armazenamento

### <a name="what-key-vault-manages"></a>O que o Key Vault gerencia

O Key Vault executa várias funções de gerenciamento interno em seu nome quando você usa Chaves de Conta de Armazenamento.

1. O Azure Key Vault gerencia chaves de uma ASA (Conta de Armazenamento do Azure). 
    - Internamente, o Azure Key Vault pode listar (sincronizar) chaves com uma Conta de Armazenamento do Azure.  
    - Gera novamente o Cofre de chaves do Azure (gira) Olá chaves periodicamente. 
    - Valores de chave nunca são retornados na resposta toocaller. 
    - O Azure Key Vault gerencia chaves tanto de Contas de Armazenamento quanto de Contas de Armazenamento Clássicas. 
2. Cofre de chaves do Azure permite que você, Olá cofre/objeto proprietário, toocreate definições de SAS (conta ou serviço SAS). 
    - Olá valor SAS, criado usando a definição de SAS, é retornado como um segredo por meio do caminho do URI de REST de saudação. Para obter mais informações, consulte [Operações de conta de armazenamento do Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).

### <a name="naming-guidance"></a>Diretrizes de nomenclatura

Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.  
 
Um nome de definição de SAS deve ter de 1 a 102 caracteres, contendo somente 0–9, a–z, A–Z.

## <a name="developer-experience"></a>Experiência do desenvolvedor 

### <a name="before-azure-key-vault-storage-keys"></a>Antes das chaves de armazenamento do Azure Key Vault 

Os desenvolvedores usavam tooneed toodo Olá seguir práticas recomendadas com uma conta tooget chave acesso tooAzure de armazenamento. 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Depois das chaves de armazenamento do Azure Key Vault 

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
 
 ### <a name="developer-best-practices"></a>Melhores práticas do desenvolvedor 

- Permita somente a suas chaves ASA toomanage de Cofre de chaves. Não tente toomanage-los por conta própria, você irá interferir com processos do cofre da chave. 
- Não permita ASA chaves toobe gerenciado por mais de um objeto de Cofre de chaves. 
- Se você precisar toomanually regenerar suas chaves ASA, recomendamos que você regenerá-los por meio do Cofre de chaves. 

## <a name="getting-started"></a>Introdução

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Configuração para permissões de RBAC (controle de acesso baseadas em função)

Cofre de chaves precisa de permissões muito*lista* e *regenerar* chaves para uma conta de armazenamento. Configure permissões utilizando Olá etapas a seguir:

- Obter ObjectId do Key Vault: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Atribua função de operador de chave de armazenamento tooAzure identidade de Cofre de chave: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Para um tipo de conta clássico, defina o parâmetro de função de saudação muito*"Clássico armazenamento chave operador serviço de função de conta"*.

### <a name="storage-account-onboarding"></a>Integração da conta de armazenamento 

Exemplo: Como um proprietário de objeto de Cofre de chaves que você adicionar um armazenamento de conta objeto tooyour Azure Key Vault tooonboard uma conta de armazenamento.

Durante a integração, o Cofre de chaves precisa tooverify se identidade Olá da conta de integração Olá também tem permissões*lista* e muito*regenerar* chaves de armazenamento. Em ordem tooverify essas permissões, o Cofre de chaves obtém um OBO (em nome de) token do serviço de autenticação hello, público definido tooAzure Gerenciador de recursos e torna um *lista* serviço de armazenamento do Azure toohello chamada de chave. Se hello *lista* chamada falhar, Olá Falha na criação do objeto com um código de status do HTTP para o Cofre de chaves *proibido*. chaves de saudação listadas dessa maneira são armazenados em cache com o armazenamento de entidade do Cofre de chaves. 

Cofre de chaves deve verificar se tem identidade Olá *regenerar* permissões antes que ele pode apropriar-se de regenerar as chaves. tooverify que Olá identidade, via token OBO, bem como Olá identidade de terceiros primeiro cofre de chaves com essas permissões:

- Cofre de chaves lista permissões de RBAC no recurso de conta de armazenamento hello.
- Cofre de chaves valida resposta Olá por meio de ações e ações de não correspondência da expressão regular. 

Encontre alguns exemplos de suporte em [Key Vault – Amostras de Chaves de Conta de Armazenamento Gerenciado](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).

Se não tiver a identidade de saudação *regenerar* permissões ou se a primeira identidade de terceiros do cofre da chave não tiver *lista* ou *regenerar* permissão, em seguida, Olá integração Falha na solicitação retornando um código de erro apropriado e uma mensagem. 

token OBO Olá só funcionará quando você usa o primário, os aplicativos cliente nativos do PowerShell ou CLI.

## <a name="other-applications"></a>Outros aplicativos

- Tokens SAS, construídas usando chaves de conta de armazenamento de Cofre de chaves, fornecem mais acesso controlado tooan conta de armazenamento do Azure. Para obter mais informações, confira [Como usar assinaturas de acesso compartilhado](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>Consulte também

- [Sobre chaves, segredos e certificados](https://docs.microsoft.com/rest/api/keyvault/)
- [Blog da equipe do Key Vault](https://blogs.technet.microsoft.com/kv/)
