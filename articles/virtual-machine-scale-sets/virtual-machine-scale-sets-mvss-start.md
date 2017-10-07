---
title: "modelos de conjunto de aaaLearn sobre escala de máquinas virtuais | Microsoft Docs"
description: "Saiba toocreate uma escala mínima de viável definir modelo para conjuntos de escala de máquinas virtuais"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>Saiba mais sobre os modelos do conjunto de dimensionamento de máquinas virtuais
[Modelos do Gerenciador de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) é uma ótima maneira toodeploy grupos de recursos relacionados. Esta série de tutorial mostra como o modelo de conjunto de toocreate uma escala viável mínima e toomodify toosuit esse modelo vários cenários. Todos os exemplos foram obtidos neste [repositório GitHub](https://github.com/gatneil/mvss). 

Este modelo é pretendido toobe simples. Para obter exemplos mais completos de escala configurar modelos, consulte Olá [repositório GitHub de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) e procure as pastas que contêm a cadeia de caracteres hello `vmss`.

Se você já estiver familiarizado com a criação de modelos, você pode ignorar toohello "Próximas etapas" seção toosee como toomodify este modelo.

## <a name="review-hello-template"></a>Modelo de saudação de revisão

Use GitHub tooreview nosso escala viável mínima definir modelo, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).

Neste tutorial, podemos examinar Olá diff (`git diff master minimum-viable-scale-set`) escala viável mínima de saudação toocreate parte por parte de modelo de conjunto.

## <a name="define-schema-and-contentversion"></a>Definir $schema e contentVersion
Primeiro, definimos `$schema` e `contentVersion` no modelo de saudação. Olá `$schema` elemento define Olá versão de idioma do modelo hello e é usado para o realce de sintaxe do Visual Studio e recursos semelhantes de validação. Olá `contentVersion` elemento não será usado pelo Azure. Em vez disso, ele ajuda a manter o controle de versão do modelo de saudação.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>Definir parâmetros
Em seguida, definimos dois parâmetros, `adminUsername` e `adminPassword`. Os parâmetros são valores que você especificou em tempo de saudação da implantação. Olá `adminUsername` parâmetro é simplesmente uma `string` tipo, mas porque `adminPassword` é um segredo, dê-tipo `securestring`. Posteriormente, esses parâmetros são passados na configuração do conjunto de escala hello.

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>Definir variáveis
Modelos do Gerenciador de recursos também permitem que você defina variáveis toobe usado posteriormente no modelo de saudação. Nosso exemplo não usa todas as variáveis, portanto deixamos objeto JSON de saudação vazio.

```json
  "variables": {},
```

## <a name="define-resources"></a>Definir recursos
Next é a seção de recursos de saudação do modelo de saudação. Aqui, você define o que você realmente deseja toodeploy. Ao contrário de `parameters` e `variables` (que são objetos JSON), `resources` é uma lista JSON de objetos JSON.

```json
   "resources": [
```

Todos os recursos exigem propriedades `type`, `name`, `apiVersion` e `location`. O primeiro recurso desse exemplo tem o tipo `Microsft.Network/virtualNetwork`, o nome `myVnet` e a apiVersion `2016-03-30`. (toofind hello mais recente versão da API para um tipo de recurso, consulte Olá [documentação da API REST do Azure](https://docs.microsoft.com/rest/api/).)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>Especificar o local
local de saudação toospecify para rede virtual hello, usamos um [função de Gerenciador de recursos de modelo](../azure-resource-manager/resource-group-template-functions.md). Essa função deve ser colocada entre aspas e colchetes desta forma: `"[<template-function>]"`. Nesse caso, usamos Olá `resourceGroup` função. Ele usa nenhum argumento e retorna um objeto JSON com metadados sobre o grupo de recursos de saudação que esta implantação está sendo implantada. grupo de recursos de saudação é definido pelo usuário Olá no tempo de saudação da implantação. Então, o índice para esse objeto JSON com `.location` tooget local de saudação do objeto JSON de saudação.

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>Especificar as propriedades da rede virtual
Cada recurso do Gerenciador de recursos tem seu próprio `properties` seção para recurso de toohello específico de configurações. Nesse caso, podemos especificar essa rede virtual Olá deve ter uma sub-rede usando o intervalo de endereços IP privado Olá `10.0.0.0/16`. Um conjunto de dimensionamento sempre está contido em uma sub-rede. Ele não pode abranger sub-redes.

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>Adicionar a lista dependsOn
Além disso toohello necessário `type`, `name`, `apiVersion`, e `location` propriedades de cada recurso podem ter um opcional `dependsOn` lista de cadeias de caracteres. Essa lista especifica quais outros recursos dessa implantação devem ser concluídos antes da implantação desse recurso.

Nesse caso, há apenas um elemento na lista de hello, rede virtual de saudação do exemplo anterior de saudação. Podemos especificar essa dependência porque Olá conjunto de escala precisa Olá tooexist de rede antes de criar todas as máquinas virtuais. Dessa forma, conjunto de escala Olá pode dar essas VMs endereços IP do intervalo de endereços IP de saudação especificado anteriormente Olá propriedades de rede. formato de saudação de cada cadeia de caracteres na lista de dependsOn Olá é `<type>/<name>`. Use Olá mesmo `type` e `name` usado anteriormente na definição de recurso de rede virtual hello.

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>Especificar as propriedades do conjunto de dimensionamento
Conjuntos de escala têm muitas propriedades para personalizar a saudação VMs no conjunto de escala de saudação. Para obter uma lista completa dessas propriedades, consulte Olá [documentação da API REST do conjunto de escala](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set). Para este tutorial, definiremos apenas algumas propriedades mais usadas.
### <a name="supply-vm-size-and-capacity"></a>Fornecer o tamanho e a capacidade da VM
Olá conjunto de escala de necessidades tooknow o tamanho da VM toocreate ("nome do sku") e quantos essa VMs toocreate ("capacidade de sku"). toosee quais tamanhos VM estão disponíveis, consulte Olá [documentação de tamanhos de VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>Escolher o tipo de atualizações
conjunto de escala Olá também precisa tooknow como toohandle atualiza no conjunto de escala de saudação. Atualmente, há duas opções, `Manual` e `Automatic`. Para obter mais informações sobre diferenças de saudação entre hello dois, consulte a documentação do hello em [como tooupgrade uma conjunto de escala](./virtual-machine-scale-sets-upgrade-scale-set.md).

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>Escolher o sistema operacional da VM
Olá conjunto de escala necessidades tooknow tooput o sistema operacional em VMs hello. Aqui, podemos criar VMs de Olá com uma imagem de 16.04 LTS Ubuntu totalmente atualizada.

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>Especificar computerNamePrefix
conjunto de escala Olá implanta várias VMs. Em vez de especificar o nome de cada VM, especificamos `computerNamePrefix`. Hello conjunto de escala acrescenta um prefixo de toohello de índice para cada VM para nomes de VM tem formulário Olá `<computerNamePrefix>_<auto-generated-index>`.

Olá trecho de código a seguir, usamos parâmetros de saudação do antes de tooset Olá administrador username e password para todas as VMs no conjunto de escala de saudação. Podemos fazer isso com hello `parameters` modelo de função. Essa função assume uma cadeia de caracteres que especifica quais tooand toorefer de parâmetro gera o valor de saudação para esse parâmetro.

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>Especificar a configuração de rede da VM
Por fim, precisamos configuração de rede toospecify Olá para Olá VMs no conjunto de escala de saudação. Nesse caso, precisamos apenas toospecify Olá ID de sub-rede Olá criado anteriormente. Isso informa Olá conjunto de escala tooput interfaces de rede Olá nesta sub-rede.

Você pode obter ID de saudação da rede virtual hello, que contém a sub-rede hello usando Olá `resourceId` modelo de função. Essa função usa o tipo de saudação e o nome de um recurso e retorna Olá identificador totalmente qualificado do recurso. Essa ID tem o formato de saudação:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

No entanto, Olá identificador de rede virtual Olá não é suficiente. Você deve especificar a sub-rede específica Olá Olá conjunto de escala de que máquinas virtuais devem estar no. toodo, concatenar `/subnets/mySubnet` toohello ID da rede virtual hello. resultado de saudação é Olá totalmente qualificado ID de sub-rede de saudação. Fazer essa concatenação com hello `concat` função, que usa uma série de cadeias de caracteres e retorna sua concatenação.

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
