---
title: "aaaDeploy várias instâncias dos recursos do Azure | Microsoft Docs"
description: "Use a operação de cópia e matrizes em um tooiterate de modelo do Azure Resource Manager várias vezes ao implantar os recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>Implantar várias instâncias de um recurso ou propriedade nos modelos do Azure Resource Manager
Este tópico mostra como tooiterate no seu toocreate de modelo do Azure Resource Manager várias instâncias de um recurso ou várias instâncias de uma propriedade em um recurso.

Se você precisar de modelo de tooyour de lógica de tooadd que permite que você toospecify se um recurso é implantado, consulte [condicionalmente implantar recursos](#conditionally-deploy-resource).

## <a name="resource-iteration"></a>Iteração de recurso
toocreate várias instâncias de um tipo de recurso, adicione um `copy` tipo de recurso do elemento toohello. No elemento de cópia hello, você especifica o número de saudação de iterações e um nome para este loop. valor de contagem de saudação deve ser um inteiro positivo e não pode exceder 800. Gerenciador de recursos cria recursos Olá em paralelo. Portanto, a ordem de saudação na qual eles são criados não é garantida. recursos toocreate iterada em sequência, consulte [cópia Serial](#serial-copy). 

Olá recurso toocreate várias vezes usa Olá formato a seguir:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

Observe que Olá Olá inclui o nome de cada recurso `copyIndex()` função, que retorna a iteração atual Olá em loop hello. `copyIndex()`é baseado em zero. Portanto, Olá exemplo a seguir:

```json
"name": "[concat('storage', copyIndex())]",
```

Cria estes nomes:

* storage0
* storage1
* storage2.

valor do índice toooffset hello, você pode passar um valor na função de copyIndex() hello. Hello número de iterações tooperform ainda está especificado no elemento de cópia hello, mas o valor Olá copyIndex tem um deslocamento de saudação especificada valor. Portanto, Olá exemplo a seguir:

```json
"name": "[concat('storage', copyIndex(1))]",
```

Cria estes nomes:

* storage1
* storage2
* storage3

operação de cópia de saudação é útil ao trabalhar com matrizes, porque você pode iterar por meio de cada elemento na matriz de saudação. Saudação de uso `length` função na contagem de saudação do hello matriz toospecify iterações, e `copyIndex` tooretrieve Olá atual índice Olá matriz. Portanto, Olá exemplo a seguir:

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

Cria estes nomes:

* storagecontoso
* storagefabrikam
* storagecoho

## <a name="serial-copy"></a>Cópia serial

Quando você usar Olá cópia elemento toocreate várias instâncias de um tipo de recurso, Gerenciador de recursos, por padrão, implanta essas instâncias em paralelo. No entanto, talvez você queira toospecify que Olá recursos são implantados em sequência. Por exemplo, ao atualizar um ambiente de produção, talvez você queira toostagger Olá para que apenas um determinado número de atualizações são atualizadas a qualquer momento.

Gerenciador de recursos fornece propriedades que permitem que você tooserially no elemento de cópia Olá implantar várias instâncias. No elemento de cópia hello, defina `mode` muito**serial** e `batchSize` toohello o número de instâncias toodeploy por vez. Com o modo serial, Gerenciador de recursos cria uma dependência em instâncias anteriores no loop hello, para um lote não será iniciado até que o lote anterior Olá for concluído.

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

Olá propriedade mode também aceita **paralela**, que é o valor padrão de saudação.

tootest serial cópia sem criar recursos reais, use Olá modelo que implanta modelos aninhados vazios a seguir:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

Em Histórico de implantação hello, observe que Olá implantações aninhadas são processados em sequência.

![implantação serial](./media/resource-group-create-multiple/serial-copy.png)

Para um cenário mais realista, Olá exemplo a seguir implanta duas instâncias em um período de uma VM do Linux de um modelo aninhado:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a>Iteração de propriedade

toocreate vários valores para uma propriedade em um recurso, adicione um `copy` matriz no elemento de propriedades de saudação. Essa matriz contém objetos, e cada objeto tem Olá propriedades a seguir:

* Olá - nome da saudação propriedade toocreate vários valores para
* Contagem - número de saudação de valores toocreate
* entrada - um objeto que contém a propriedade Olá values tooassign toohello  

Olá mostrado no exemplo a seguir como tooapply `copy` toohello dataDisks propriedade em uma máquina virtual:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Observe que ao usar `copyIndex` dentro de uma iteração de propriedade, você deve fornecer o nome de saudação de iteração hello. Você não tem nome de saudação tooprovide quando usado com a iteração de recurso.

Gerenciador de recursos expande Olá `copy` matriz durante a implantação. nome de saudação da matriz de saudação se torna o nome de saudação da propriedade hello. os valores de entrada Hello tornam-se propriedades do objeto hello. modelo de saudação implantado se torna:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Você pode usar iteração de recurso e propriedade juntos. Iteração de propriedade de saudação de referência por nome.

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

Você só pode incluir um elemento de cópia nas propriedades de saudação de cada recurso. toospecify um loop de iteração para mais de uma propriedade, definir vários objetos na matriz de cópia de saudação. Cada objeto é iterado separadamente. Por exemplo, toocreate várias instâncias de ambos os hello `frontendIPConfigurations` propriedade e hello `loadBalancingRules` propriedade em um balanceador de carga, definir ambos os objetos em um elemento de cópia única: 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a>Depender dos recursos em um loop
Você especifica que um recurso é implantado depois de outro recurso com hello `dependsOn` elemento. toodeploy um recurso que depende de coleção de saudação de recursos em um loop, forneça o nome de saudação do loop de cópia Olá no elemento de dependsOn hello. saudação de exemplo a seguir mostra como toodeploy três contas de armazenamento antes de implantar Olá a máquina Virtual. definição completa de máquina Virtual Olá não é mostrada. Observe que esse elemento de cópia Olá tem nome definido muito`storagecopy` e elemento dependsOn Olá Olá máquinas virtuais também está definido muito`storagecopy`.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a>Criar diversas instâncias de um recurso filho
Você não pode usar um loop de cópia para um recurso filho. toocreate várias instâncias de um recurso que você normalmente define como aninhadas dentro de outro recurso, você deve criar esse recurso como um recurso de nível superior. Definir relação Olá com recurso de pai Olá por meio das propriedades de tipo e o nome da saudação.

Por exemplo, suponha que você normalmente defina um conjunto de dados como um recurso filho em uma data factory.

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

toocreate várias instâncias de conjuntos de dados, movê-lo fora da fábrica de dados hello. saudação de conjunto de dados deve estar no hello mesmo nível como fábrica de dados hello, mas ainda é um recurso filho Olá da fábrica de dados. Preservar a relação de saudação entre conjunto de dados e a fábrica de dados por meio das propriedades de tipo e o nome da saudação. Desde que o tipo não pode ser inferido de sua posição no modelo Olá, você deve fornecer o tipo hello totalmente qualificado no formato Olá: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.

tooestablish uma relação pai/filho com uma instância da fábrica de dados Olá, forneça um nome para Olá conjunto de dados que inclui o nome do recurso pai hello. Use o formato de saudação: `{parent-resource-name}/{child-resource-name}`.  

Olá, exemplo a seguir mostra a implementação de saudação:

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a>Implantar o recurso condicionalmente

toospecify se um recurso for implantado, use Olá `condition` elemento. valor desse elemento Olá resolve tootrue ou false. Quando Olá valor for true, o recurso de saudação é implantado. Quando Olá valor for false, o recurso de saudação não está implantado. Por exemplo, toospecify se uma nova conta de armazenamento é implantada ou uma conta de armazenamento existente é usada, use:

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

Para obter um exemplo do uso de um recurso novo ou existente, consulte [Modelo de condição novo ou existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

Para obter um exemplo do uso de uma senha ou a máquina de virtual toodeploy chave SSH, consulte [modelo de condição de nome de usuário ou o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="next-steps"></a>Próximas etapas
* Se você quiser toolearn sobre seções de saudação de um modelo, consulte [criação de modelos de Gerenciador de recursos do Azure](resource-group-authoring-templates.md).
* toolearn como toodeploy seu modelo, consulte [implantar um aplicativo com o modelo do Gerenciador de recursos do Azure](resource-group-template-deploy.md).

