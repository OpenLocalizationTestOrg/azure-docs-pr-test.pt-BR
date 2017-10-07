---
title: "ordem de implantação de aaaSet para recursos do Azure | Microsoft Docs"
description: "Descreve como um recurso tooset como depende de outro recurso durante tooensure os recursos de implantação são implantados na ordem correta hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Defina a ordem de saudação para implantar recursos em modelos do Gerenciador de recursos do Azure
Para um determinado recurso, pode haver outros recursos que devem existir antes da implantação de recursos de saudação. Por exemplo, um SQL server deve existir antes de tentar toodeploy um banco de dados SQL. Definir esta relação marcando um recurso como dependente Olá outro recurso. Definir uma dependência com hello **dependsOn** elemento, ou usando Olá **referência** função. 

Gerenciador de recursos avalia Olá dependências entre os recursos e implanta-os em sua ordem dependente. Quando os recursos não dependem uns dos outros, o Gerenciador de Recursos os implanta paralelamente. Você só precisa de toodefine dependências de recursos que são implantados em Olá mesmo modelo. 

## <a name="dependson"></a>dependsOn
Dentro de seu modelo, Olá dependsOn elemento permite que você toodefine um recurso como um dependente em um ou mais recursos. Seu valor pode ser uma lista de nomes de recurso separados por vírgula. 

Olá, exemplo a seguir mostra um conjunto de escala de máquina virtual depende de um balanceador de carga de rede virtual e um loop que cria várias contas de armazenamento. Esses outros recursos não são mostrados no exemplo a seguir de saudação, mas precisam tooexist em outro lugar no modelo de saudação.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

No hello anterior de exemplo, uma dependência está incluída nos recursos de saudação que são criados por meio de um loop de cópia chamado **storageLoop**. Por exemplo, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md)

Ao definir dependências, você pode incluir Olá recurso provedor namespace e o recurso tipo tooavoid ambiguidade. Por exemplo, tooclarify de formato de um balanceador de carga e rede virtual que pode ter Olá que mesmos nomes, como outros recursos, use Olá a seguir:

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

Embora você possa estar toouse decidido dependsOn toomap relações entre os recursos, é importante toounderstand por que você está fazendo. Por exemplo, toodocument como os recursos são interconectados, dependsOn não é abordagem certa hello. Não é possível consultar os recursos que foram definidos no elemento de dependsOn Olá após a implantação. Ao usar o dependsOn, você potencialmente afeta o tempo de implantação, pois o Resource Manager não implanta paralelamente dois recursos que têm uma dependência. toodocument relações entre os recursos, em vez disso, use [vinculação de recursos](/rest/api/resources/resourcelinks).

## <a name="child-resources"></a>Recursos filho
propriedade de recursos Olá permite recursos filho toospecify que sejam toohello relacionados do recurso que está sendo definido. Os recursos filho só podem ser definidos em cinco níveis de profundidade. É importante toonote uma dependência implícita não é criada entre um recurso filho e o recurso pai de saudação. Se precisar hello filho recurso toobe implantado após o recurso pai de hello, deve declarar explicitamente essa dependência com a propriedade de dependsOn hello. 

Cada recurso pai aceita somente determinados tipos de recurso como recursos filho. Olá aceita tipos de recurso são especificados em Olá [esquema de modelo](https://github.com/Azure/azure-resource-manager-schemas) do recurso pai de saudação. nome de saudação filho do tipo de recurso inclui o nome de saudação do tipo de recurso pai hello, como **Microsoft.Web/sites/config** e **Microsoft.Web/sites/extensions** são ambos os recursos filho de saudação  **Microsoft.Web/sites**.

saudação de exemplo a seguir mostra um SQL server e banco de dados SQL. Observe que uma dependência explícita é definida entre o banco de dados do hello SQL e SQL server, mesmo que o banco de dados de saudação é um filho do servidor de saudação.

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>Função reference
Olá [fazem referência a função](resource-group-template-functions-resource.md#reference) permite que uma expressão tooderive seu valor de outros pares de nome e valor JSON ou recursos de tempo de execução. Expressões de referência declaram de maneira implícita que um recurso depende de outro. formato de saudação geral é:

```json
reference('resourceName').propertyPath
```

Em Olá exemplo a seguir, um ponto de extremidade CDN depende explicitamente Olá perfil CDN e implicitamente depende de um aplicativo web.

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

Você pode usar este elemento ou Olá dependsOn elemento toospecify as dependências, mas você não precisa toouse ambos para Olá mesmo recurso dependente. Sempre que possível, use um tooavoid referência implícita adicionando uma dependência desnecessária.

mais, consulte toolearn [fazem referência a função](resource-group-template-functions-resource.md#reference).

## <a name="recommendations-for-setting-dependencies"></a>Recomendações para a configuração de dependências

Ao decidir qual tooset dependências, use Olá diretrizes a seguir:

* Defina o mínimo de dependências possível.
* Defina um recurso filho como dependente do recurso pai.
* Saudação de uso **referência** tooset dependências de implícita entre os recursos que precisam de tooshare uma propriedade de função. Não adicione uma dependência explícita (**dependsOn**) quando você já definiu uma dependência implícita. Essa abordagem reduz o risco de saudação de ter dependências desnecessárias. 
* Defina uma dependência quando um recurso não pode ser **criado** sem funcionalidades de outro recurso. Não defina uma dependência se recursos Olá interagem somente após a implantação.
* Coloque as dependências em cascata sem defini-las explicitamente. Por exemplo, sua máquina virtual depende de uma interface de rede virtual e interface de rede virtual Olá depende de uma rede virtual e endereços IP públicos. Portanto, máquina virtual de saudação é implantados depois que todos os três recursos, mas não defina explicitamente Olá VM como dependentes em todos os três recursos. Essa abordagem esclarece a ordem de dependência hello e torna mais fácil do modelo de saudação toochange mais tarde.
* Se um valor pode ser determinado antes da implantação, tente implantar recursos de saudação sem uma dependência. Por exemplo, se um valor de configuração precisa de nome de saudação de outro recurso, talvez não seja necessário uma dependência. Este guia não funciona sempre porque alguns recursos Verifique a existência de saudação do hello outro recurso. Se você receber um erro, adicione uma dependência. 

O Resource Manager identifica dependências circulares durante a validação do modelo. Se você receber um erro indicando que existe uma dependência circular, avalie sua toosee de modelo se qualquer dependência não é necessários e pode ser removida. Se remover dependências não funcionar, você pode evitar dependências circulares ao mover algumas operações de implantação em recursos filho que são implantados após recursos Olá com dependência circular hello. Por exemplo, suponha que você está implantando duas máquinas virtuais, mas você deve definir propriedades em cada um deles que se referem a outros toohello. Você pode implantá-los em Olá ordem a seguir:

1. vm1
2. vm2
3. Extensão na vm1 depende vm1 e vm2. extensão de saudação define valores na vm1 obtém da vm2.
4. Extensão da vm2 depende vm1 e vm2. extensão de saudação define valores vm2 obtém da vm1.

Para obter informações sobre como avaliar uma ordem de implantação hello e resolver erros de dependência, consulte [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre dependências de solução de problemas durante a implantação, consulte [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn sobre como criar modelos do Azure Resource Manager, consulte [criar modelos](resource-group-authoring-templates.md). 
* Para obter uma lista das funções disponíveis do hello em um modelo, consulte [funções de modelo](resource-group-template-functions.md).

