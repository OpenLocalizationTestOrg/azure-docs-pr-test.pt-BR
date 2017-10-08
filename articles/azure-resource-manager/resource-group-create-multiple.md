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
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="4f9fd-103">Implantar várias instâncias de um recurso ou propriedade nos modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4f9fd-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="4f9fd-104">Este tópico mostra como tooiterate no seu toocreate de modelo do Azure Resource Manager várias instâncias de um recurso ou várias instâncias de uma propriedade em um recurso.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="4f9fd-105">Se você precisar de modelo de tooyour de lógica de tooadd que permite que você toospecify se um recurso é implantado, consulte [condicionalmente implantar recursos](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="4f9fd-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="4f9fd-106">Iteração de recurso</span><span class="sxs-lookup"><span data-stu-id="4f9fd-106">Resource iteration</span></span>
<span data-ttu-id="4f9fd-107">toocreate várias instâncias de um tipo de recurso, adicione um `copy` tipo de recurso do elemento toohello.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="4f9fd-108">No elemento de cópia hello, você especifica o número de saudação de iterações e um nome para este loop.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="4f9fd-109">valor de contagem de saudação deve ser um inteiro positivo e não pode exceder 800.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="4f9fd-110">Gerenciador de recursos cria recursos Olá em paralelo.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="4f9fd-111">Portanto, a ordem de saudação na qual eles são criados não é garantida.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="4f9fd-112">recursos toocreate iterada em sequência, consulte [cópia Serial](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="4f9fd-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="4f9fd-113">Olá recurso toocreate várias vezes usa Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-113">hello resource toocreate multiple times takes hello following format:</span></span>

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

<span data-ttu-id="4f9fd-114">Observe que Olá Olá inclui o nome de cada recurso `copyIndex()` função, que retorna a iteração atual Olá em loop hello.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="4f9fd-115">`copyIndex()`é baseado em zero.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="4f9fd-116">Portanto, Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="4f9fd-117">Cria estes nomes:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-117">Creates these names:</span></span>

* <span data-ttu-id="4f9fd-118">storage0</span><span class="sxs-lookup"><span data-stu-id="4f9fd-118">storage0</span></span>
* <span data-ttu-id="4f9fd-119">storage1</span><span class="sxs-lookup"><span data-stu-id="4f9fd-119">storage1</span></span>
* <span data-ttu-id="4f9fd-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-120">storage2.</span></span>

<span data-ttu-id="4f9fd-121">valor do índice toooffset hello, você pode passar um valor na função de copyIndex() hello.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="4f9fd-122">Hello número de iterações tooperform ainda está especificado no elemento de cópia hello, mas o valor Olá copyIndex tem um deslocamento de saudação especificada valor.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="4f9fd-123">Portanto, Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="4f9fd-124">Cria estes nomes:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-124">Creates these names:</span></span>

* <span data-ttu-id="4f9fd-125">storage1</span><span class="sxs-lookup"><span data-stu-id="4f9fd-125">storage1</span></span>
* <span data-ttu-id="4f9fd-126">storage2</span><span class="sxs-lookup"><span data-stu-id="4f9fd-126">storage2</span></span>
* <span data-ttu-id="4f9fd-127">storage3</span><span class="sxs-lookup"><span data-stu-id="4f9fd-127">storage3</span></span>

<span data-ttu-id="4f9fd-128">operação de cópia de saudação é útil ao trabalhar com matrizes, porque você pode iterar por meio de cada elemento na matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="4f9fd-129">Saudação de uso `length` função na contagem de saudação do hello matriz toospecify iterações, e `copyIndex` tooretrieve Olá atual índice Olá matriz.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="4f9fd-130">Portanto, Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-130">So, hello following example:</span></span>

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

<span data-ttu-id="4f9fd-131">Cria estes nomes:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-131">Creates these names:</span></span>

* <span data-ttu-id="4f9fd-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="4f9fd-132">storagecontoso</span></span>
* <span data-ttu-id="4f9fd-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="4f9fd-133">storagefabrikam</span></span>
* <span data-ttu-id="4f9fd-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="4f9fd-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="4f9fd-135">Cópia serial</span><span class="sxs-lookup"><span data-stu-id="4f9fd-135">Serial copy</span></span>

<span data-ttu-id="4f9fd-136">Quando você usar Olá cópia elemento toocreate várias instâncias de um tipo de recurso, Gerenciador de recursos, por padrão, implanta essas instâncias em paralelo.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="4f9fd-137">No entanto, talvez você queira toospecify que Olá recursos são implantados em sequência.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="4f9fd-138">Por exemplo, ao atualizar um ambiente de produção, talvez você queira toostagger Olá para que apenas um determinado número de atualizações são atualizadas a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="4f9fd-139">Gerenciador de recursos fornece propriedades que permitem que você tooserially no elemento de cópia Olá implantar várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="4f9fd-140">No elemento de cópia hello, defina `mode` muito**serial** e `batchSize` toohello o número de instâncias toodeploy por vez.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="4f9fd-141">Com o modo serial, Gerenciador de recursos cria uma dependência em instâncias anteriores no loop hello, para um lote não será iniciado até que o lote anterior Olá for concluído.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="4f9fd-142">Olá propriedade mode também aceita **paralela**, que é o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="4f9fd-143">tootest serial cópia sem criar recursos reais, use Olá modelo que implanta modelos aninhados vazios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="4f9fd-144">Em Histórico de implantação hello, observe que Olá implantações aninhadas são processados em sequência.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![implantação serial](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="4f9fd-146">Para um cenário mais realista, Olá exemplo a seguir implanta duas instâncias em um período de uma VM do Linux de um modelo aninhado:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

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

## <a name="property-iteration"></a><span data-ttu-id="4f9fd-147">Iteração de propriedade</span><span class="sxs-lookup"><span data-stu-id="4f9fd-147">Property iteration</span></span>

<span data-ttu-id="4f9fd-148">toocreate vários valores para uma propriedade em um recurso, adicione um `copy` matriz no elemento de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="4f9fd-149">Essa matriz contém objetos, e cada objeto tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="4f9fd-150">Olá - nome da saudação propriedade toocreate vários valores para</span><span class="sxs-lookup"><span data-stu-id="4f9fd-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="4f9fd-151">Contagem - número de saudação de valores toocreate</span><span class="sxs-lookup"><span data-stu-id="4f9fd-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="4f9fd-152">entrada - um objeto que contém a propriedade Olá values tooassign toohello</span><span class="sxs-lookup"><span data-stu-id="4f9fd-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="4f9fd-153">Olá mostrado no exemplo a seguir como tooapply `copy` toohello dataDisks propriedade em uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="4f9fd-154">Observe que ao usar `copyIndex` dentro de uma iteração de propriedade, você deve fornecer o nome de saudação de iteração hello.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="4f9fd-155">Você não tem nome de saudação tooprovide quando usado com a iteração de recurso.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="4f9fd-156">Gerenciador de recursos expande Olá `copy` matriz durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="4f9fd-157">nome de saudação da matriz de saudação se torna o nome de saudação da propriedade hello.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="4f9fd-158">os valores de entrada Hello tornam-se propriedades do objeto hello.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-158">hello input values become hello object properties.</span></span> <span data-ttu-id="4f9fd-159">modelo de saudação implantado se torna:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-159">hello deployed template becomes:</span></span>

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

<span data-ttu-id="4f9fd-160">Você pode usar iteração de recurso e propriedade juntos.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="4f9fd-161">Iteração de propriedade de saudação de referência por nome.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-161">Reference hello property iteration by name.</span></span>

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

<span data-ttu-id="4f9fd-162">Você só pode incluir um elemento de cópia nas propriedades de saudação de cada recurso.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="4f9fd-163">toospecify um loop de iteração para mais de uma propriedade, definir vários objetos na matriz de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="4f9fd-164">Cada objeto é iterado separadamente.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-164">Each object is iterated separately.</span></span> <span data-ttu-id="4f9fd-165">Por exemplo, toocreate várias instâncias de ambos os hello `frontendIPConfigurations` propriedade e hello `loadBalancingRules` propriedade em um balanceador de carga, definir ambos os objetos em um elemento de cópia única:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="4f9fd-166">Depender dos recursos em um loop</span><span class="sxs-lookup"><span data-stu-id="4f9fd-166">Depend on resources in a loop</span></span>
<span data-ttu-id="4f9fd-167">Você especifica que um recurso é implantado depois de outro recurso com hello `dependsOn` elemento.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="4f9fd-168">toodeploy um recurso que depende de coleção de saudação de recursos em um loop, forneça o nome de saudação do loop de cópia Olá no elemento de dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="4f9fd-169">saudação de exemplo a seguir mostra como toodeploy três contas de armazenamento antes de implantar Olá a máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="4f9fd-170">definição completa de máquina Virtual Olá não é mostrada.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="4f9fd-171">Observe que esse elemento de cópia Olá tem nome definido muito`storagecopy` e elemento dependsOn Olá Olá máquinas virtuais também está definido muito`storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="4f9fd-172">Criar diversas instâncias de um recurso filho</span><span class="sxs-lookup"><span data-stu-id="4f9fd-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="4f9fd-173">Você não pode usar um loop de cópia para um recurso filho.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="4f9fd-174">toocreate várias instâncias de um recurso que você normalmente define como aninhadas dentro de outro recurso, você deve criar esse recurso como um recurso de nível superior.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="4f9fd-175">Definir relação Olá com recurso de pai Olá por meio das propriedades de tipo e o nome da saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="4f9fd-176">Por exemplo, suponha que você normalmente defina um conjunto de dados como um recurso filho em uma data factory.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="4f9fd-177">toocreate várias instâncias de conjuntos de dados, movê-lo fora da fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="4f9fd-178">saudação de conjunto de dados deve estar no hello mesmo nível como fábrica de dados hello, mas ainda é um recurso filho Olá da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="4f9fd-179">Preservar a relação de saudação entre conjunto de dados e a fábrica de dados por meio das propriedades de tipo e o nome da saudação.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="4f9fd-180">Desde que o tipo não pode ser inferido de sua posição no modelo Olá, você deve fornecer o tipo hello totalmente qualificado no formato Olá: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="4f9fd-181">tooestablish uma relação pai/filho com uma instância da fábrica de dados Olá, forneça um nome para Olá conjunto de dados que inclui o nome do recurso pai hello.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="4f9fd-182">Use o formato de saudação: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="4f9fd-183">Olá, exemplo a seguir mostra a implementação de saudação:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-183">hello following example shows hello implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="4f9fd-184">Implantar o recurso condicionalmente</span><span class="sxs-lookup"><span data-stu-id="4f9fd-184">Conditionally deploy resource</span></span>

<span data-ttu-id="4f9fd-185">toospecify se um recurso for implantado, use Olá `condition` elemento.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="4f9fd-186">valor desse elemento Olá resolve tootrue ou false.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="4f9fd-187">Quando Olá valor for true, o recurso de saudação é implantado.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="4f9fd-188">Quando Olá valor for false, o recurso de saudação não está implantado.</span><span class="sxs-lookup"><span data-stu-id="4f9fd-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="4f9fd-189">Por exemplo, toospecify se uma nova conta de armazenamento é implantada ou uma conta de armazenamento existente é usada, use:</span><span class="sxs-lookup"><span data-stu-id="4f9fd-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="4f9fd-190">Para obter um exemplo do uso de um recurso novo ou existente, consulte [Modelo de condição novo ou existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="4f9fd-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="4f9fd-191">Para obter um exemplo do uso de uma senha ou a máquina de virtual toodeploy chave SSH, consulte [modelo de condição de nome de usuário ou o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="4f9fd-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f9fd-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4f9fd-192">Next steps</span></span>
* <span data-ttu-id="4f9fd-193">Se você quiser toolearn sobre seções de saudação de um modelo, consulte [criação de modelos de Gerenciador de recursos do Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4f9fd-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="4f9fd-194">toolearn como toodeploy seu modelo, consulte [implantar um aplicativo com o modelo do Gerenciador de recursos do Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4f9fd-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

