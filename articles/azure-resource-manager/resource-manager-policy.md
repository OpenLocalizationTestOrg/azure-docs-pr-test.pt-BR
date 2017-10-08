---
title: "políticas de recursos aaaAzure | Microsoft Docs"
description: "Descreve como as propriedades de recurso consistente do toouse do Azure Resource Manager políticas tooensure são definidas durante a implantação. Políticas podem ser aplicadas a grupos de assinatura ou o recurso de saudação."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>Visão geral de políticas de recursos
Políticas de recursos permitem que você tooestablish convenções para recursos em sua organização. Definindo as convenções, você pode controlar os custos e muito mais fácil gerenciar seus recursos. Por exemplo, você pode especificar que somente determinados tipos de máquinas virtuais são permitidos. Ou você pode exigir que todos os recursos tenham uma marca específica. As políticas são herdadas por todos os recursos filho. Portanto, se uma política for aplicada tooa grupo de recursos, é aplicável tooall recursos de saudação desse grupo de recursos.

Há dois toounderstand conceitos sobre as políticas de:

* definição de política - descrevem quando a política de saudação é imposta e qual ação tootake
* atribuição de política - aplicar Olá política definição tooa escopo (assinatura ou grupo de recursos)

Este tópico se concentra na definição de política. Para obter informações sobre atribuição de política, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md) ou [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).

Políticas são avaliadas durante a criação e atualização de recursos (PUT e operações de PATCHES).

> [!NOTE]
> Atualmente, política não avalia os tipos de recursos que não oferecem suporte a marcas, tipo e local, como o tipo de recurso de Microsoft.Resources/deployments hello. Esse suporte será adicionado no futuro. tooavoid problemas de compatibilidade com versões anteriores, você deve especificar explicitamente as tipo ao criar políticas. Por exemplo, uma política de marcação que não especifica tipos é aplicada a todos os tipos. Nesse caso, uma implantação de modelo poderá falhar se houver um recurso aninhado que não oferece suporte a marcas e tipo de recurso de implantação de saudação foi adicionado toopolicy avaliação. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>Qual é a diferença dela em relação ao RBAC?
Há algumas diferenças importantes entre a política e o RBAC (controle de acesso baseado em função). O RBAC se concentra nas ações do **usuário** em escopos diferentes. Por exemplo, você é adicionados toohello a função de Colaborador para um grupo de recursos no escopo de saudação desejado, para que você pode fazer alterações toothat grupo de recursos. Diretiva enfoca **recursos** propriedades durante a implantação. Por exemplo, por meio de políticas, você pode controlar os tipos de saudação de recursos que podem ser provisionados. Ou, você pode restringir os locais Olá no qual recursos Olá podem ser provisionados. Ao contrário do RBAC, a política é um sistema de permissão padrão e negação explícita. 

políticas de toouse, você deve ser autenticado por meio de RBAC. Especificamente, a conta precisa de:

* `Microsoft.Authorization/policydefinitions/write`permissão toodefine uma política
* `Microsoft.Authorization/policyassignments/write`permissão tooassign uma política 

Essas permissões não são incluídas no hello **Colaborador** função.

## <a name="built-in-policies"></a>Políticas internas

O Azure fornece algumas definições de políticas internas que podem reduzir o número de saudação de políticas de você ter toodefine. Antes de continuar com as definições de política, você deve considerar se uma política interna já fornece definição Olá que necessária. definições de políticas internas de saudação são:

* Locais permitidos
* Tipos de recursos permitidos
* SKUs de contas de armazenamento permitidas
* SKUs de máquinas virtuais permitidas
* Aplicar a marca e o valor padrão
* Impor a marca e o valor
* Tipos de recursos não permitidos
* Requer o SQL Server versão 12.0
* Exigir criptografia de conta de armazenamento

Você pode atribuir qualquer essas políticas por meio de saudação [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), ou [CLI do Azure](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>Estrutura da definição de política
Use o JSON toocreate uma definição de política. definição de política de saudação contém elementos para:

* parâmetros
* nome de exibição
* descrição
* regra de política
  * avaliação de lógica
  * efeito

saudação de exemplo a seguir mostra uma diretiva que limita quais recursos são implantados:

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>parâmetros
Usando parâmetros ajuda a simplificar o gerenciamento de política reduzindo Olá número de definições de política. Definir uma política para uma propriedade de recurso (como limitar onde os recursos podem ser implantados de locais de saudação) e incluir parâmetros na definição de saudação. Em seguida, reutilize essa definição de política para diferentes cenários passando valores diferentes (por exemplo, a especificação de um conjunto de locais para uma assinatura) quando a atribuição de diretiva de saudação.

Declare parâmetros ao criar definições de política.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

tipo de saudação de um parâmetro pode ser um cadeia de caracteres ou matriz. propriedade de metadados de saudação é usada para as ferramentas como informações amigáveis toodisplay portal do Azure. 

Na regra de política de saudação, você fazer referência a parâmetros com hello sintaxe a seguir: 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Nome de exibição e descrição

Use Olá **displayName** e **descrição** tooidentify Olá definição de política e fornecer contexto para quando ele é usado.

## <a name="policy-rule"></a>Regra de política

regra de política de saudação consiste em **se** e **, em seguida,** blocos. Em Olá **se** bloco, você define uma ou mais condições que especificam quando a política de saudação é imposta. Você pode aplicar os operadores lógicos toothese condições tooprecisely definir cenário Olá para uma política. Em Olá **, em seguida,** bloco, definir o efeito de saudação que acontece quando hello **se** condições sejam cumpridas.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>Operadores lógicos
operadores lógicos Olá com suporte são:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

Olá **não** sintaxe inverte o resultado de saudação da condição de saudação. Olá **allOf** sintaxe (semelhante toohello lógica **e** operação) requer true de toobe todas as condições. Olá **nenhum** sintaxe (semelhante toohello lógica **ou** operação) requer um ou mais true de toobe de condições.

Você pode aninhar operadores lógicos. Olá mostrado no exemplo a seguir um **não** operação é aninhada dentro de uma **allOf** operação. 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a>Condições
Olá condição avalia se um **campo** atenda a certos critérios. condições de saudação com suporte são:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Ao usar o hello **como** condição, você pode fornecer um curinga (*) no valor de saudação.

Ao usar o hello **corresponder** condição, fornecer `#` toorepresent um dígito, `?` para uma letra e qualquer outro caractere toorepresent esse caractere real. Para obter exemplos, consulte [Aplicar políticas de recursos para nomes e texto](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Campos
As condições são formadas usando campos. Um campo representa as propriedades na carga de solicitação de recurso de saudação que é o estado de saudação toodescribe usado do recurso de saudação.  

Olá campos a seguir têm suporte:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* aliases de propriedade - para obter uma lista, confira [Aliases](#aliases).

### <a name="effect"></a>Efeito
A política dá suporte a três tipos de efeito - `deny`, `audit` e `append`. 

* **Negar** gera um evento no log de auditoria de saudação e falha de solicitação de saudação
* **Auditoria** gera um evento de aviso no log de auditoria, mas não falha solicitação Olá
* **Acrescentar** adiciona Olá definido pelo conjunto de campos toohello solicitação 

Para **acrescentar**, você deve fornecer Olá detalhes a seguir:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

valor de saudação pode ser uma cadeia de caracteres ou um objeto no formato JSON. 

## <a name="aliases"></a>Aliases

Você pode usar aliases tooaccess específico de propriedades para um tipo de recurso. Aliases permitem que você toorestrict quais valores ou condições são permitidas para uma propriedade em um recurso. Cada alias mapeia toopaths em diferentes versões de API para um tipo de recurso específico. Durante a avaliação de política, o mecanismo de políticas de saudação obtém caminho da propriedade Olá para essa versão de API.

**Microsoft.Cache/Redis**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Defina se da porta do servidor de Redis de não ssl hello (6379) está habilitado. |
| Microsoft.Cache/Redis/shardCount | Definir o número de saudação de fragmentos toobe criado em um Cache de Cluster Premium.  |
| Microsoft.Cache/Redis/sku.capacity | Definir tamanho de saudação do hello Redis cache toodeploy.  |
| Microsoft.Cache/Redis/sku.family | Definir toouse família de SKU de saudação. |
| Microsoft.Cache/Redis/sku.name | Definir o tipo de saudação da Cache Redis toodeploy. |

**Microsoft.Cdn/profiles**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Definir nome Olá Olá preço. |

**Microsoft.Compute/disks**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Definir oferta Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/imagePublisher | Definida publisher Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/imageSku | Olá conjunto SKU de imagem da plataforma hello ou imagem do marketplace usado toocreate Olá VM. |
| Microsoft.Compute/imageVersion | Defina a versão de saudação do hello plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |


**Microsoft.Compute/virtualMachines**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Compute/imageId | Identificador de saudação da máquina virtual do hello imagem usada toocreate saudação do conjunto. |
| Microsoft.Compute/imageOffer | Definir oferta Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/imagePublisher | Definida publisher Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/imageSku | Olá conjunto SKU de imagem da plataforma hello ou imagem do marketplace usado toocreate Olá VM. |
| Microsoft.Compute/imageVersion | Defina a versão de saudação do hello plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/licenseType | Defina essa imagem hello ou o disco está licenciado no local. Esse valor é usado apenas para imagens que contêm o sistema de operacional de servidor do Windows hello.  |
| Microsoft.Compute/virtualMachines/imageOffer | Definir oferta Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/virtualMachines/imagePublisher | Definida publisher Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/virtualMachines/imageSku | Olá conjunto SKU de imagem da plataforma hello ou imagem do marketplace usado toocreate Olá VM. |
| Microsoft.Compute/virtualMachines/imageVersion | Defina a versão de saudação do hello plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Defina o vhd Olá URI. |
| Microsoft.Compute/virtualMachines/sku.name | Definir tamanho de saudação da máquina virtual de saudação. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Definir nome de saudação do editor da extensão hello. |
| Microsoft.Compute/virtualMachines/extensions/type | Definir o tipo de saudação da extensão. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Defina a versão de saudação da extensão de saudação. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Compute/imageId | Identificador de saudação da máquina virtual do hello imagem usada toocreate saudação do conjunto. |
| Microsoft.Compute/imageOffer | Definir oferta Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/imagePublisher | Definida publisher Olá Olá plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/imageSku | Olá conjunto SKU de imagem da plataforma hello ou imagem do marketplace usado toocreate Olá VM. |
| Microsoft.Compute/imageVersion | Defina a versão de saudação do hello plataforma imagem ou marketplace imagem usada toocreate Olá máquina virtual. |
| Microsoft.Compute/licenseType | Defina essa imagem hello ou o disco está licenciado no local. Esse valor é usado apenas para imagens que contêm o sistema de operacional de servidor do Windows hello. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Defina o prefixo do nome de computador Olá para todas as máquinas virtuais de saudação no conjunto de escala de saudação. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Defina o URI do blob Olá para imagem do usuário. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Definir URLs de contêiner de saudação são discos do sistema operacional toostore usado para o conjunto de escala hello. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Defina o tamanho de saudação de máquinas virtuais em um conjunto de escala. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Camada de saudação do conjunto de máquinas virtuais em um conjunto de escala. |
  
**Microsoft.Network/applicationGateways**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Definir tamanho de saudação do gateway de saudação. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Defina o tipo de saudação desse gateway de rede virtual. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Definir nome do SKU de gateway de saudação. |

**Microsoft.Sql/servers**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Defina a versão de saudação do servidor de saudação. |

**Microsoft.Sql/databases**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Definir a edição de saudação do banco de dados de saudação. |
| Microsoft.Sql/servers/databases/elasticPoolName | Nome do conjunto de saudação do banco de dados de saudação do pool Elástico hello está em. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Olá conjunto configurado ID objetivo de nível de serviço de banco de dados de saudação. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Nome do conjunto de saudação do hello configurado objetivo de nível de serviço de banco de dados de saudação.  |

**Microsoft.Sql/elasticpools**

| Alias | Descrição |
| ----- | ----------- |
| servidores/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Total de saudação do conjunto compartilhado DTU de pool Elástico de banco de dados de saudação. |
| servidores/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Definir a edição de saudação do pool Elástico hello. |

**Microsoft.Storage/storageAccounts**

| Alias | Descrição |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Camada de acesso de saudação conjunto usada para cobrança. |
| Microsoft.Storage/storageAccounts/accountType | Nome do SKU de saudação do conjunto. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Defina se o serviço Olá criptografa os dados de saudação conforme eles são armazenados no serviço de armazenamento de blob hello. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Defina se o serviço de saudação criptografa os dados de saudação conforme eles são armazenados no serviço de armazenamento de arquivo hello. |
| Microsoft.Storage/storageAccounts/sku.name | Nome do SKU de saudação do conjunto. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Configure serviço de toostorage de tráfego de https apenas tooallow. |


## <a name="policy-examples"></a>Exemplos de políticas

Olá tópicos a seguir contêm exemplos de política:

* Para obter exemplos de políticas de marca, veja [Aplicar políticas de recursos para marcas](resource-manager-policy-tags.md).
* Para obter exemplos de padrões de nomenclatura e texto, confira [Aplicar políticas de recursos a nomes e texto](resource-manager-policy-naming-convention.md).
* Para obter exemplos de políticas de armazenamento, consulte [se aplicam a contas do recurso políticas toostorage](resource-manager-policy-storage.md).
* Para obter exemplos de políticas de máquina virtual, consulte [aplicar políticas de recursos tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) e [aplicar políticas de recursos tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>Próximas etapas
* Depois de definir uma regra de política, atribua-tooa escopo. políticas de tooassign por meio do portal hello, consulte [tooassign portal do Azure de uso e gerenciar políticas de recursos](resource-manager-policy-portal.md). políticas de tooassign por meio da API REST, PowerShell ou CLI do Azure, consulte [atribuir e gerenciar políticas por meio de script](resource-manager-policy-create-assign.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).
* esquema de política de saudação é publicado em [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

