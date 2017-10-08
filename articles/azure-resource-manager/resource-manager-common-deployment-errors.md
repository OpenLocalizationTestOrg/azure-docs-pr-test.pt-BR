---
title: "erros comuns de implantação do Azure aaaTroubleshoot | Microsoft Docs"
description: "Descreve como erros comuns de tooresolve quando você implanta tooAzure de recursos usando o Gerenciador de recursos do Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Erro de implantação, implantação do azure, implantar tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Solução de erros comuns de implantação do Azure com o Azure Resource Manager
Este tópico descreve como é possível resolver alguns erros de implantação comuns do Azure que você pode encontrar.

Olá códigos de erro a seguir é descrita neste tópico:

* [AccountNameInvalid](#accountnameinvalid)
* [Falha na autorização](#authorization-failed)
* [BadRequest](#badrequest)
* [DeploymentFailed](#deploymentfailed)
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink)
* [InvalidTemplate](#invalidtemplate)
* [MissingSubscriptionRegistration](#noregisteredproviderfound)
* [NotFound](#notfound)
* [NoRegisteredProviderFound](#noregisteredproviderfound)
* [OperationNotAllowed](#quotaexceeded)
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded)
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy)
* [ResourceNotFound](#notfound)
* [SkuNotAvailable](#skunotavailable)
* [StorageAccountAlreadyExists](#storagenamenotunique)
* [StorageAccountAlreadyTaken](#storagenamenotunique)

## <a name="deploymentfailed"></a>DeploymentFailed

Esse código de erro indica um erro de implantação geral, mas não é código de erro Olá precisar toostart de solução de problemas. código de erro de saudação que realmente ajuda você a resolver o problema de saudação geralmente é um nível abaixo desse erro. Por exemplo, hello imagem a seguir mostra Olá **RequestDisallowedByPolicy** código de erro que está sob o erro de implantação de saudação.

![mostrar código de erro](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

Ao implantar um recurso (normalmente uma máquina virtual), você pode receber Olá mensagem de erro e o código de erro a seguir:

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

Você recebe esse erro quando o recurso Olá SKU selecionado (por exemplo, o tamanho da VM) não está disponível para o local de saudação selecionado. tooresolve esse problema, você precisa toodetermine que SKUs estão disponíveis em uma região. Você pode usar o PowerShell, Olá portal ou um toofind da operação REST SKUs disponíveis.

- Para o PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) e filtre por localização. Você deve ter a versão mais recente de saudação do PowerShell para este comando.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  resultados da saudação incluem uma lista de SKUs para o local do hello e as restrições para a SKU.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- Olá toouse [portal](https://portal.azure.com), faça logon no portal de toohello e adicionar um recurso por meio da interface de saudação. Como definir os valores hello, você vê Olá SKUs disponíveis para esse recurso. Implantação de saudação toocomplete não é necessário.

    ![SKUs disponíveis](./media/resource-manager-common-deployment-errors/view-sku.png)

- Olá toouse API REST para máquinas virtuais, enviar Olá solicitação a seguir:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Ele retorna disponível SKUs e regiões no hello formato a seguir:

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

Se você não é possível toofind uma SKU adequada na região ou uma região alternativa que atenda às suas necessidades de negócios, enviar um [solicitação SKU](https://aka.ms/skurestriction) tooAzure suporte.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

Se você receber esse erro, você está usando uma assinatura que não é permitido tooaccess todos os serviços do Azure que não sejam do Active Directory do Azure. Você pode ter esse tipo de assinatura quando você precisar portal clássico do tooaccess hello, mas não é permitidas toodeploy recursos. tooresolve esse problema, você deve usar uma assinatura que tem permissão toodeploy recursos.  

tooview suas assinaturas disponíveis com o PowerShell, use:

```powershell
Get-AzureRmSubscription
```

E assinatura atual tooset hello, use:

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview suas assinaturas disponíveis com o Azure 2.0 do CLI, use:

```azurecli
az account list
```

E assinatura atual tooset hello, use:

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Esse erro pode resultar de vários tipos diferentes de erros.

- Erro de sintaxe

   Se você receber uma mensagem de erro que indica a validação do modelo falha hello, você pode ter um problema de sintaxe em seu modelo.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Esse erro é fácil toomake como expressões de modelo podem ser complexas. Por exemplo, hello seguinte atribuição de nome de uma conta de armazenamento contém um conjunto de colchetes, três funções, três conjuntos de parênteses, um conjunto de aspas simples e uma propriedade:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Se você não fornecer uma sintaxe de correspondência de Olá, o modelo Olá produz um valor que é diferente de sua intenção.

   Quando você receber esse tipo de erro, revise atentamente a sintaxe de expressão hello. Considere usar um editor JSON como o [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) ou o [Visual Studio Code](resource-manager-vs-code.md) que pode avisá-lo sobre os erros de sintaxe.

- Comprimentos de segmento incorretos

   Outro erro de modelo inválida ocorre quando o nome do recurso Olá não está no formato correto de saudação.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Um recurso no nível raiz deve ter um segmento de menos em nome de saudação que no tipo de recurso de saudação. Cada segmento é diferenciado por uma barra. Olá exemplo a seguir, o tipo de saudação possui dois segmentos e nome de saudação tem um segmento, portanto, é um **nome válido**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Mas Olá próximo exemplo é **não é um nome válido** porque ele tem Olá mesmo número de segmentos que tipo de saudação.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Para obter recursos filho, Olá tipo e o nome tem Olá mesmo número de segmentos. Esse número de segmentos faz sentido, porque o nome completo do hello e tipo filho Olá inclui o tipo e o nome do pai de saudação. Portanto, nome completo Olá ainda tem um menor do segmento de tipo completo hello.

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   Obtendo segmentos de saudação à direita podem ser complicados com tipos de Gerenciador de recursos que são aplicados em todos os provedores de recursos. Por exemplo, a aplicação de um site da web de tooa de bloqueio de recurso requer um tipo com quatro segmentos. Portanto, o nome de saudação é três segmentos:

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- O índice de cópia não é esperado

   Você encontrar isso **InvalidTemplate** erro quando você aplicou Olá **cópia** parte de tooa do elemento do modelo de saudação que não oferece suporte a esse elemento. Só é possível aplicar o tipo de recurso do hello cópia elemento tooa. Não é possível aplicar cópia tooa propriedade dentro de um tipo de recurso. Por exemplo, você aplicar cópia tooa virtual machine, mas você não pode aplicar toohello OS discos para uma máquina virtual. Em alguns casos, você pode converter um filho toocreate de recursos pai do recurso tooa um loop de cópia. Para obter mais informações sobre como usar a cópia, consulte [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).

- O parâmetro não é válido

   Se o modelo Olá Especifica os valores permitidos para um parâmetro, e você fornecer um valor que não é um desses valores, você receberá um toohello semelhante de mensagem erro a seguir:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   Olá verifique valores permitidos no modelo de saudação e fornecê-lo durante a implantação.

- Dependência circular detectada

   Você recebe esse erro quando recursos dependem uns aos outros de forma que impede a implantação de saudação de iniciar. Uma combinação de interdependências faz com que dois ou mais recursos aguardar para outros recursos que também estão aguardando. Por exemplo, recurso1 depende resource3 resource2 depende recurso1 e resource3 depende resource2. Geralmente você pode resolver esse problema removendo dependências desnecessárias. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound e ResourceNotFound
Quando o modelo inclui nome de saudação de um recurso que não pode ser resolvido, você recebe um erro semelhante a:

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Se você estiver tentando Olá toodeploy recurso no modelo de saudação ausente, verifique se é necessário tooadd uma dependência. O Gerenciador de Recursos otimiza a implantação criando recursos em paralelo, quando possível. Se um recurso deve ser implantado após outro recurso, você precisa Olá toouse **dependsOn** toocreate seu modelo uma dependência no elemento Olá outro recurso. Por exemplo, ao implantar um aplicativo web, Olá plano de serviço de aplicativo deve existir. Se você não especificou que o aplicativo web hello depende Olá plano de serviço de aplicativo, o Gerenciador de recursos cria os recursos no hello simultaneamente. Você recebe um erro informando que Olá não é possível encontrar o recurso de plano de serviço de aplicativo, porque ele ainda não existir durante a tentativa de tooset uma propriedade no aplicativo web de saudação. Evitar esse erro, definindo a dependência de saudação no aplicativo web de saudação.

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

Para obter sugestões sobre como solucionar erros de dependência, veja [Verificar a sequência de implantação](#check-deployment-sequence).

Você também ver esse erro quando recursos Olá existe em outro grupo de recursos que Olá um sendo implantado. Nesse caso, use Olá [função resourceId](resource-group-template-functions-resource.md#resourceid) tooget nome totalmente qualificado do hello do recurso de saudação.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Se você tentar Olá toouse [referência](resource-group-template-functions-resource.md#reference) ou [listkeys do](resource-group-template-functions-resource.md#listkeys) funções com um recurso que não pode ser resolvida, você receberá Olá erro a seguir:

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Procure por uma expressão que inclui Olá **referência** função. Verifique se os valores de parâmetro hello estão corretos.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

Quando um recurso é um recurso de tooanother do pai, recurso pai de saudação deve existir antes de criar o recurso de filho hello. Se ele ainda não existir, você receberá Olá erro a seguir:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

nome de saudação do recurso de filho Olá inclui nome de pai de hello. Por exemplo, um Banco de Dados SQL pode ser definido como:

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Mas, se você não especificar uma dependência no recurso pai, Olá, recurso filho de saudação pode obter implantado antes do pai de saudação. tooresolve esse erro incluem uma dependência.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists e StorageAccountAlreadyTaken
Para contas de armazenamento, você deve fornecer um nome para o recurso de saudação que é exclusivo no Azure. Se você não fornecer um nome exclusivo, receberá um erro como:

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

Você pode criar um nome exclusivo, concatenando a convenção de nomenclatura com resultado Olá Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) função.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Se você implantar uma conta de armazenamento com hello o mesmo nome como uma conta de armazenamento existente na sua assinatura, mas fornecem um local diferente, você receberá um erro indicando que conta de armazenamento Olá já existe em um local diferente. Exclua a conta de armazenamento existente hello ou fornecer Olá mesmo local como Olá conta de armazenamento existente.

## <a name="accountnameinvalid"></a>AccountNameInvalid
Consulte Olá **AccountNameInvalid** erro ao tentar toogive um armazenamento de conta um nome que contenha caracteres proibidos. Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres, usar números e apenas letras minúsculas. Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) função retorna 13 caracteres. Se você concatenar um prefixo toohello **uniqueString** resultados, forneça um prefixo de 11 caracteres ou menos.

## <a name="badrequest"></a>BadRequest

Você pode receber um status BadRequest ao fornecer um valor inválido para uma propriedade. Por exemplo, se você fornecer um valor incorreto do SKU para uma conta de armazenamento, implantação de saudação falhará. os valores válidos para a propriedade, toodetermine examinar Olá [API REST](/rest/api) para tipo de recurso Olá você está implantando.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound e MissingSubscriptionRegistration
Durante a implantação de recursos, você pode receber Olá após o código de erro e mensagem:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Ou você poderá receber uma mensagem semelhante que indica:

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

Você recebe esses erros por um dos três motivos:

1. provedor de recursos de saudação não foi registrado para sua assinatura
2. Versão de API não tem suportada para o tipo de recurso Olá
3. Local não tem suportada para o tipo de recurso Olá

mensagem de erro de saudação deve fornecer sugestões para locais de saudação com suporte e as versões de API. Você pode alterar sua tooone do modelo de saudação valores sugeridos. A maioria dos provedores são registradas automaticamente pelo Olá interface de linha de comando de portal ou hello Azure você está usando, mas não todas. Se você não tiver usado um provedor de recursos específico antes, talvez seja necessário tooregister esse provedor. Você pode descobrir mais sobre provedores de recursos por meio do PowerShell ou CLI do Azure.

**Portal**

Você pode ver o status de registro hello e registrar um namespace de provedor de recursos por meio do portal hello.

1. Em sua assinatura, selecione **Provedores de recursos**.

   ![selecionar provedores de recursos](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Examinar a lista de saudação de provedores de recursos e, se necessário, selecione Olá **registrar** provedor de recursos do link tooregister saudação do tipo hello tentar toodeploy.

   ![listar provedores de recursos](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee o status do registro, use **Get-AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

tooregister um provedor, use **AzureRmResourceProvider registro** e forneça o nome de saudação do provedor de recursos de saudação desejar tooregister.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

locais de saudação suporte tooget para um determinado tipo de recurso, use:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Olá tooget versões de API com suporte para um determinado tipo de recurso, use:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**CLI do Azure**

toosee se Olá provedor está registrado, use Olá `azure provider list` comando.

```azurecli
az provider list
```

tooregister um provedor de recursos, use Olá `azure provider register` de comando e especificar Olá *namespace* tooregister.

```azurecli
az provider register --namespace Microsoft.Cdn
```

locais de saudação suporte toosee e as versões de API para um tipo de recurso, use:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded e OperationNotAllowed
Você pode ter problemas quando a implantação ultrapassar uma cota, que pode ser por grupo de recursos, assinaturas, contas e outros escopos. Por exemplo, sua assinatura pode ser configurada toolimit Olá número de núcleos de uma região. Se você tentar toodeploy uma máquina virtual com mais núcleos do que Olá permitido valor, você receber um erro informando a saudação cota foi excedida.
Para obter informações completas sobre cotas, consulte [Limites, cotas e restrições de serviço e assinatura do Azure](../azure-subscription-service-limits.md).

tooexamine cotas de sua assinatura para núcleos, você pode usar o hello `azure vm list-usage` do hello CLI do Azure. saudação de exemplo a seguir ilustra essa cota de núcleo Olá para uma conta de avaliação gratuita é 4:

```azurecli
az vm list-usage --location "South Central US"
```

Que retorna:

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

Se você implantar um modelo que cria mais de quatro núcleos na região Oeste dos EUA de Olá, você receberá um erro de implantação que se parece com:

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

Ou no PowerShell, você pode usar o hello **AzureRmVMUsage Get** cmdlet.

```powershell
Get-AzureRmVMUsage
```

Que retorna:

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

Nesses casos, você deve ir toohello portal e a cota de região Olá no qual você deseja toodeploy um tooraise do problema de suporte do arquivo.

> [!NOTE]
> Lembre-se de que grupos de recursos, cota Olá para cada região, não para a assinatura inteira hello. Se você precisar de núcleos de 30 toodeploy no Oeste dos EUA, você terá tooask para 30 núcleos do Gerenciador de recursos no Oeste dos EUA. Se você precisar de núcleos de 30 toodeploy em qualquer Olá regiões toowhich você tem acesso, você deve pedir 30 núcleos do Gerenciador de recursos em todas as regiões.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Quando você receber a mensagem de saudação do erro:

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

Você tentou provavelmente toolink tooa modelo aninhado que não está disponível. Verifique hello URI fornecido para o modelo aninhado hello. Se o modelo de saudação existir em uma conta de armazenamento, certifique-se de Olá URI está acessível. Talvez seja necessário toopass um token SAS. Para saber mais, confira [Usando modelos vinculados com o Gerenciador de Recursos do Azure](resource-group-linked-templates.md).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
Você recebe esse erro quando sua assinatura inclui uma política de recurso que impede que uma ação que você está tentando tooperform durante a implantação. Na mensagem de erro hello, procure o identificador de política de saudação.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

Em **PowerShell**, forneça esse identificador de política como Olá **Id** detalhes do parâmetro tooretrieve sobre a política de saudação que bloqueou a sua implantação.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

Em **CLI do Azure**, forneça o nome de saudação da definição de política de saudação:

```azurecli
az policy definition show --name regionPolicyAssignment
```

Para obter mais informações, consulte Olá artigos a seguir:

- [Erro RequestDisallowedByPolicy](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [Usar os recursos de toomanage de política e controlar o acesso](resource-manager-policy.md).

## <a name="authorization-failed"></a>Falha na autorização
Você pode receber um erro durante a implantação porque hello conta ou entidade de tentativa de recursos de saudação toodeploy de serviço não tem acesso tooperform essas ações. Active Directory do Azure permite que você ou sua toocontrol administrador quais identidades podem acessar os recursos com um alto grau de precisão. Por exemplo, se sua conta é atribuída a função de leitor toohello, você não é toocreate capaz de recursos. Nesse caso, você vê uma mensagem de erro indicando que houve falha na autorização.

Para obter mais informações sobre o controle de acesso baseado em funções, consulte [Controle de Acesso Baseado em Funções do Azure](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Próximas etapas
* toolearn sobre a auditoria de ações, consulte [operações com o Gerenciador de recursos de auditoria](resource-group-audit.md).
* toolearn sobre erros de saudação toodetermine ações durante a implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).
